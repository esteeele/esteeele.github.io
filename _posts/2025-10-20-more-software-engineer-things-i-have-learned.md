---
layout: post
title:  "More things I've learned about developing enterprise software"
date:   2025-10-19 12:00:18 +0000
categories: [software]
---

In the past year I’ve become increasingly senior at my job, being pushed into more engagement with various stakeholders at a large, UK fintech. While earlier in my career I worked very closely with product managers and leadership at a much smaller company, there’s a world of difference to working with large teams who are extremely removed from software development. 

This post tries to encapsulate what I’ve learned, or has further been reinforced recently. 

## 'Soft' Skills

Soft Skills as you become more senior (unless you're a super specialised developer) become probably more important than tech ones, or at least the line becomes horribly blurred, for doing your job.

### Understanding different ways of thinking 

*Engineers have a different mindset to business stakeholders*

For business stakeholders the main reason for praise/prestige tends to be around identifying problems. 

Engineers are praised for solving problems. 

Trying to get a mix of both is crucial - but doing too much of one and not enough of the other is an issue. Too much problem identification tends towards circular conversations without a resolution. Engineers diving too soon into coming up with solutions can risk creating fixes to problems that don’t really exist - or even worse than that building subtly incorrectly mis-modelling real world business logic. 

Here team work and effective communication is crucial. All meetings should have an intended outcome, and engineers should either understand the domain well enough to model it correctly, or product managers need to step in. 

### Dealing with timelines

Engineering is unusual in that success is based on timelines rather than outcomes. This is an endless problem that everyone struggles with, because generally we create a thing and it’s just assumed to be essentially bug free, highly available and easy to modify and change. It’s important to stress that (especially as a company’s tech stack grows and matures) that this stuff isn’t “free” and will require work. This can stray into coming up with Non-Functional Requirements - which in my opinion are showing things going slightly wrong, because it’s a kind of imposition of restrictive categoric data onto what is often quite ephemeral. I.e. do I feel this software is nice to work with? 

The best way lies in building up personal relationships and trust between you and others and hoping that your judgement and expertise will be trusted. If it’s not, and it’s impossible then you potentially work at a chop shop and it’s time to move on. In the worst case pushing back more aggressively with comments meant to illustrate the difficulty of delivering to timelines can help (but be careful) e.g. _It would be unfair to ask you (sales) what exactly what date you expect to sign (customer) because we are interested in outcomes rather than timelines._ The idea here is to point out an absurdity we often see e.g. _in March having a conversation where you commit to having features 1..50 on the spreadsheet all being in place at 9AM on the 17th September._


### Stakeholders abhor a vacuum 

So this is something I’ve seen over and over again in my career. The nature of software development work (especially at early stages of a project but really throughout) means it’s hard to communicate what’s really going on.  Often it can look from the outside like no progress is being made - in early stage design, during periods of heavier refactoring - then suddenly everything happens at once. 

The issue is that if you’re not upfront about what’s going on business leaders will often assume the worse, especially if you’re not in a high trust environment. What’s being asked for is so so often totally reasonable - just a few bullet points about what the team has been doing, what’s been challenging etc.. In many cases ‘micromanagement’ comes from this communication vacuum, where a middle manager isn’t certain of what’s happening, is being leant on my a senior manager who has no idea what’s happening. If you can send bite sized chunks of useful information up that chain it’ll keep managers happy and off your back. (In an ideal world)  

### Looking after developers in your team (if not a people manager)

It’s vital to learn how to delegate well. 9 times out of 10 people don’t know exactly what you’re doing, or even how best to help you with the workload - you can’t just drop work onto people’s lap and immediately expect them to get started. Delegation can often take time away initially but pays itself back over time. 

Give Praise: This one is huge, especially for new starters or people who may lack confidence. Software Engineering can be lonely at times, and quite negative
- Dealing with customer reported issues 
- Pushing back on timelines and “disappointing” other people in the business 
- An often challenging and esoteric job we do a lot of in isolation 

In a way that may not be obvious people (especially but not exclusively juniors) have massive imposter syndrome which can become a deeply negative feedback loop. 
- I’m not good enough to do this work 
- So I’ll do something else, or not trust my judgement and get someone else to do the hard parts 
- So I don’t improve and gain confidence 
- So my imposter syndrome sticks around 

While doing a kind of Big Tech AI _Wow - What an interesting and intelligent insight that gets right to the heart of …_ doesn’t help anyone because its obviously disingenuous - remembering to give praise where its earned makes a huge difference. For example if you’re reviewing a PR that has a couple of minor issues but is overall OK then remember to include the praise for the 90% that’s good. Dropping a comment to praise specific things you think are smart can also give a lot of encouragement. 

## Technical Learnings

### Do not ever drift along and push 'First draft' code into production 

If I think about what’s gone well in the past year compared to what’s gone badly its when a “rough and ready” prototype has survived all the way into production, only to become a giant pain in the neck but increasingly hard to modify as customer data builds up. 

The issue is basically down to not building a data model that makes sense and/or a set of abstractions that match the kind of behaviour you’re looking for your application. Why this happens tends to relate to: 
- timelines that don’t (seem to) give developers time to refactor and re-model code to make better, 
- a lack of teamwork where no-one feels empowered to make sweeping changes so an inferior design persists, 
- developers not understanding the product domain well enough.

All you can do yourself is fight this if it happens - push back if necessary (every time I’ve done this business stakeholders have been totally happy) to give pauses in feature delivery to make tactical and thoughtful changes for a couple of weeks.  In your team be the change you want to see - try and build working relationships and a high trust environment (own up to mistakes, be friendly and share credit). For design work if no-one is stepping into that role - great that means you’re up and it’s the best way to learn. If your plans crash and burn at least you’ve learned something! 

In my experience knowingly putting a design developers aren’t happy with in production is the worst way to tank team morale, delivery and trust with the rest of the business. 

### Time saved in testing is paid for many times over

This one is pretty simple and kind of a no-brainer. Test as many paths as is practical, especially, especially the unhappy paths. Add good automated ‘integration tests’ that test flows as a whole from the perspective of the end-client (e.g. a mobile device) to see if the disparate parts of your application are well glued together. Sending silly mistakes into non-prod environments that need to be reverted just wastes time. 

Never send code to production you haven’t given a manual once over in demo. 

The other risk for you personally as a senior developer is that you are "on-call" as far as many non-developers in the business are concerned. For example even if a bug or issue in production originates in a part of an application you have no idea about, you're the one who's going to be contacted about it because people know who you are. This can be a real mental burden and result in excessive context switching and exhaustion. This is why it is vital and in your own personal interest to keep as many issues off production as you possibly can. 

### Overseeing implementation of something you’ve designed, but are not the primary implementer for.

The example: This year I designed an async process that was a version of the classic manager/worker pattern where a series of tasks happen and eventually some entity is pushed through a state machine. To ensure consistency each worked could only make one transactional write to the database after fetching some data or making a modification to a remote service. 

This is something I’ve found difficult. At earlier stages of my career what I’ve done tended to be smaller bit of functionality of APIs with a different defined purpose and scope, but as I’ve become more senior the complexity and impact of work increases. What I’ve found works well 
- Sharing very high level designs and flows using diagrams and docs. There’s not too much point going into detail at this stage as everything is so likely to change. 
- Making an initial implementation and personally creating the most crucial building blocks 
- Then ASAP have another developer extend your system, or implement interfaces required by it and get honest feedback. This is so crucial it’s hard to overstate. Software is often worthless until someone else touches it. _No plan of software attack survives first contact with someone else_ to paraphrase Von Moltke. 
- Be vigilant but not overbearing at the review stage and ongoing monitoring. 
    - At the review stage ensure the most fundamental parts of the design are being adhered to, but some freedom if it doesn’t affect the overall behaviour of the interface. 
    - Often a developer (usually senior) will not understand the design and do something that violates its purpose. A senior on the team then wrote code that mixed fetches from other services, and multiple transactions, missing that the point was to avoid a situation where one system is up, the other is down and we update data into an inconsistent state. Being a senior the more junior reviewer waved the change through (perhaps thinking _maybe they know something I don’t_). 
    - The issue here is that even if you document everything, explain it, there’s no guarantee that someone with too little time will come in and do something you don’t want. It’s your responsibility to check up and make sure you’ve done as much as you can to stop this happening. 
- Take criticism seriously but not personally. It’s extremely easy to criticise someone else’s code but this may or may not be useful criticism. It's genuinely hard to take bad faith criticism from a colleague but try not to let it get to you. Some personal anecdotes 
    - _This system is too over-engineered and hard to use_ - seems like good feedback, but really the developer didn’t fully understand the process and was just trying to slam some code in. Writing better documentation and personally explaining things helped here. 
    - _This is too hard and time consuming to setup tests for_. Ding ding: this is a huge problem and requires immediate attention to resolve. You should under no circumstances be making it hard for developers to test, because this will hammer the test coverage of new code. Resolution: Implement and refactor test preparation to make setup easy and simple, for example using a test specific data model of your system’s entities. 

### Read, read and then read some more 

I cannot overstate this enough. I would say that reading software and business books (even if tangentially related) is maybe not super exciting, but is maybe the best use of your time outside work. Once writing code is ‘easy’ the best way to upskill yourself is by reading well regarded software books. You don’t have to agree with everything these books contain, but should at least find something interesting in their pages. Some books I’ve read recently and enjoyed 
- _Designing Data-Intensive Applications: Martin Kleppmann_ (If you work with web applications you owe it to yourself to read this)
- _Why Machines Learn: Anil Ananthawamy_ (A segue to be sure but a clear and understandable dive into how machine learning actually works without getting lost in a sea of Python - quite Mathematical)
- _A Philosophy of Software Design: John Ousterhout_ 
- _The Pragmatic Programmer_ (Legendary book on "Blue Collar" coding)
- _Everything is Predicable: Tom Chivers_ (OK not at all related but a really readable fairly lightweight book on Bayesian statistics that I'd recommend to anyone)

_N.b. AI: I didn't use AI to write this. So much intelligent stuff has been written about AI in software I don't feel I have anything to add. I do feel though, for being creative, AI can hurt rather than help, as it (out of the box) tends to homogenise thought rather than let whatever you have that's unique come out. For coding though it is obviously a productivity boon._