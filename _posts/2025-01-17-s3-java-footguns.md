---
layout: post
title:  "Surprising problems with S3 and Java's InputStream"
date:   2025-01-17 18:00:18 +0000
categories: software
---

To begin with S3 is of course AWS' object storage system that abstracts the underlying realities
of actually storing files into a (mostly) intuitive and easy to use API. It's reliability and reach 
are truly staggering and it is one of the most impressive large scale software systems out there. 

But it can go wrong - there are some behaviours that are unclear, confusing and difficult. 
This is a list mainly composed of painful lessons learned the hard - code that seems innocuous
but turns around to bite you when you least expect it. This is totally from the perspective of using 
the Java client SDK. 

## InputStream (more like pain pipe)

InputStreams are a fundamental abstraction for working with byte data with the JVM from the very 
outset of the platform and are deeply ingrained in all sorts of libraries. They are, it's fair to say, 
ubiquitous.

With AWS S3 however the client gives you a nice Java bit of code like
`InputStream inputStream = s3Client.getObject(GetObjectRequest.builder().bucket("b").key("k").build())`

Then a Java developer can see something like this and write some code like 

```java
try (InputStream inputStream = s3Client.getObject(GetObjectRequest.builder().bucket("b").key("k").build())) {
    byte[] buffer = new byte[1024];
    for (int length; (length = inputStream.read(buffer)) != -1; ) {
        byte[] bytes = new byte[length];
        var string = new String(bytes, StandardCharsets.UTF_8);
        // check something about the string
        if (string.contains("something-we-dont-like")) {
            throw new RuntimeException("Uh oh");
        }
    }
} catch (IOException ioException) {
    throw new RuntimeException(ioException);
}
```

I've seen code like this in production environments and in an ordinary situation
in the JVM it is totally 100% OK. The `try()` [syntax](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html)
gives a guarantee that the stream will be _closed_.  

Another example here might be if JSON objects are being stored in S3 and read into memory - if the application
POJO 'schema' becomes incompatible with what's stored in S3 then you'd see this a lot.  

### What is wrong with this?

The key is when the exception gets thrown.
S3 is a remote server with a connection managed by HTTP! The JVM can _close_ your stream sure, but what happens
to the underlying connection? How does the multiple layers in technology know the connection is now severed? 
They don't really. All that's happened if some piped data is not being read anymore. Will it be read again soon? 
The actual HTTP connection has to wait for the default timeouts to expire before closing the connection. 

It really can catch people out that `close` here _does not_ mean closing the HTTP connection!

In a busy application then what can go badly wrong is a Java application might create a S3 client as a singleton 
with a fixed thread pool (say 50 or 100 threads). If these threads are all idling because of some nasty bug 
released in some code that parses S3 bytes then you can quickly get thread pool exhaustion, even if the 
code is 'correct' that throws the exception down the stack! 

### What could be done? 
 
1. Call the `abort()` method on `ResponseInputStream`
2. Write all data to RAM or disk everytime
3. Do not throw when processing S3 input streams. 

There's no perfect solution in my opinion. 

For 1) the issue is you can get some messy code e.g. in that example I showed earlier say I add an abort like so 
```java
if (string.contains("something-we-dont-like")) {
    inputStream.abort();
    throw new AnImportantException("Uh oh");
}
```

In _most_ cases this should be fine, but have to be aware that the `abort` is itself of course having to 
manage the underlying HTTP connection. There's a lot of moving parts there and they can and will. 
This means the exception (or just anything) in the next line isn't _guaranteed_ to throw, which can 
introduce regressions in some code bases.

The other subtler issue is slight vendor lock in. In theory the beauty of using a system like S3 is 
allowing developers to insulate themselves from the harsh reality of actually putting things onto a disk,
and this level of specificity to AWS' system is perhaps replacing one form of "essential knowledge" (how 
a disk works) with another "AWS internals". When you write Java code like this you would no longer be
passing around the widely accepted `InputStream` into your applications you'd be passing an AWS interface
with special error handling rules. 

For 2) this is probably the best outcome. If you're just piping to RAM or disk then there's far less chance anything
can go wrong when downloading the data, meaning shorter connections. There will be issues with risk around
OOMing your application or running out of disk space (probably why `InputSteam` downloads were used in 
the first place) but the trade-off is worth it in my opinion. How much does adding disk space or even RAM
add to running an application? _Is it more or less than the salary-time it takes for someone in management 
to share their screen in an all hands?_

For 3) it is so absurd to talk about, I only included to hit the "rule-of-3" in rhetoric. 


