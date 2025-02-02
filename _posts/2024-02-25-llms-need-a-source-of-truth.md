---
layout: post
title:  "LLM's will probably be a component of a truly intelligent system, not the system itself"
date:   2024-02-25 18:41:18 +0000
categories: [software]
---

LLMs, while amazingly useful in so many ways, lack a concept of truth that will hold them back unless combined with a system capable of discerning true information from hallucinations.

### The idea of “hallucinations” is a marketing gimmick.

There is no hallucination and there is no true output. A LLM produces whatever is statistically likely - in contrast a fact is not statistically likely, a fact simply is.

I’ve seen so many news reports that after listing the upside of an LLM will list the downsides, and will often list a “tendency to hallucinate” as a drawback. No. This isn’t something that can be fixed by the LLM itself. Take arithmetic - an early problem with ChatGPT was its failure to add numbers together. Thankfully this was fixed down this line by sending maths looking questions to an actual calculator. GPT didn’t ‘learn maths'; someone just added a subsystem to bypass the LLM where it was appropriate to. To fix maths in an LLM you’d need enough data covering enough arithmetic questions written in everyday language to be built into the model. Or you could just use existing arithmetic logic - something computers were built to do.

So this is a flawed example. No-one needs or wants AI to do arithmetic, that’s been a solved problem for decades now. Where we are currently seeing problems is a misapplication of AI into roles where truth is expected.

### LLMs are not search engines

I used to work with a publishing company that provided services around analysing textual data for example providing a specialist search engine. While I worked in the grubby web development team, I sat across a row of desks for the data science team. This was before the AI explosion from 2021 onwards but they were of course well aware of the developments of GPT-2 - and for the most part they understood it to be a tool for a different problem. It was understood that when someone requested data relating to a certain topic or existing content they wanted … well content related to that topic or term. They didn’t want content that _might_ relate to their query.

We’ve already seen a legal case thrown out because a lawyer trusted a response from an LLM about a non-existent case. In most cases I imagine we’re already seeing lower impact damage from researchers and analysts making mistaken conclusions from inaccurate but correct sounding output.

### LLM chatbots

This is more likely to be a flash in the pan as companies will quickly realise their mistake in allowing ChatGPT free rein to help their customers. Personally I find AI chatbots exceedingly irritating but I’ll imagine that will improve as GPT slurps up more data. Recently an LLM put one statistically likely foot in front of the other and invented a refund policy that the parent company had to honour.

This is exceptionally silly. An LLM should never have been allowed to start generating text related to a refund policy. The overall system should have detected the customer was asking about refunds and stepped in with a deterministic print out of the company’s official refund policy and probably a number to call for a human. This would imply the existence of a second regulating system on top of GPT that checks and controls inputs and outputs from the internal GPT model to ensure they make sense.

### My $0.02

So in these 3 examples we need a mind outside of GPT that can verify its responses. For now that’s us but does it have to be? Could we build a machine that is itself endogenously capable of somehow knowing what is true and what isn’t? If you’re a materialist then the answer clearly is yes - because we as biological machines can already do it. The question is how? I know actually - _but I’ll only tell you for 7 trillion USD!_

For now I think the answer is always remembering to verify anything that sounds like a fact from GPT, and for software use cases wrapping the GPT input/output away from direct external usage and carefully controlling the communication through programmed rules. Someday this may look like an anachronism but for now although GPT will inevitably get better and better as it consumes more data, it can never know what it is saying is true.
