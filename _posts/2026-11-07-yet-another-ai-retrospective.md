---
layout: post
title:  "Yet another AI retrospective"
date:   2026-11-07 12:00:18 +0000
categories: [software]
---

2026 was the year AI became the default way to write code across a lot of the industry - or at least in the web-dev, fast results commercial space I've spent my career working in. For me I've really tried to lean into using AI as well as possible (in no small part thanks to a one-off $1000 credit from Anthropic at work). 

I'd like to share some my overall thoughts, some positive and some negatives then my thoughts on the future at the end. 

To start with - I think AI is a net large positive both for the commercial software industry and for at home fun or artistic use. I still think as a whole, especially at work, we are fumbling around for the best possible usages for it. I've now had enough experience to see versions of this play out: big-data, no-sql and microservices come to mind as technologies that were rapidly adopted into innapriorpiate situations then loudly and vengefully dropped. AI feels more like The Cloud - initially mocked by some but it became more-or-less a better way for most organisations to operate. 

My personal preference for using gen-AI to give some context
- _Opus_ tier models in virtually all cases 
- I still am the primary 'typist' for most non-trivial code I touch
- Using AI to gather context and produce one-off reports is for me the biggest game-changer of the technology

I think the only thing controversial in this is not using AI to generate code in virtually all cases. While I have no actual numbers for this the results even with frontier models is still disappointing and doesn't justify the often significant costs. Reading and writing are different fundamentally different skills. As anyone who has learned a language will tell you - you can feel like an expert in reading a language, but the even after the simplest conversations you're reduced to a jabbering wreck. I think writing code isn't so different. Having to _really_ understand the domain and problem you are dealing with is for me the point of being a software engineer, by having to generate my own changes I can get a feeling for the current codebase, the product domain, that simply reading generated output doesn't give me. I would still feel the superficial feeling of understanding `claude` can give you with its writing style is dangerous. But what I am not saying is that fumbling around trying to remember particular elegant language syntax or crafting some perfect code is still the most valuable use of my time - with a clear goal and limited context most AI models are now a better coder than I am. 

So in summary - I find writing code to be the most efficient way of understanding what it is that I am doing. Others experiences may differ of course, I'm speaking for myself only. 

Aside: "spec driven development". I've basically always done this even before AI, but the old adage - _No plan of action survives first contact with the main enemy body_ - still applies. You need to get down and dirty with the detail at some point, being immersed in it helps give the necessary context. 

### Opus/Sol all the way

Opus tier models are phenomenal coders but my experience is all models still are disappointing for routine non-trivial software development work. I've tried to replicate some of the results I've seen people on the internet claim at my job but most times have failed, often burning $50+ with nothing to show for it. This is really quite puzzling when you consider these companies are solving Millennium Maths problems with similar models, and yet at the same time they can still make a mess of a simple task.

My best results have come at the low end of the cost scale - small context windows, focussed tasks, rapidly restarting if context-rot seems to be setting in. In this scenario why use _sonnet_? Yes you might save a dollar or so, but at the cost of (generally) worse quality work. 

Others have talked about this a lot but I still really hate how _opus_ uses English. Its so long winded, verbose and hard to follow. My personal system prompt has an entire paragraph with a style guide just to make it bearable.

### Is it possible to have too much productivity?

Even before AI came onto the scene it was widely acknowledged that software development is a mentally demanding job, and expecting 35-40hrs+/week of solid work is expecting too much, especially for over 25s. AI has (good) reduced to the need to do a lot of coding drudgery - e.g. setting up unit test cases, getting fiddly language specific features, refactoring. I have found though that this has meant you can spend the entire (non-meeting) day in the weeds of interesting but still challenging problems. Obviously no-one likes being bored at work but I've noticed increasingly that I have to sometimes give myself longer breaks - before a boring refactor might take 30 minutes but leave you recharged - now that job is already done. 

I'm not sure where this leads. Probably nowhere but it'd be interesting to see if the industry, especially startups, become even more youth focussed. 

### Speed or haste and does code quality still matter now?

Most commercial software companies create an environment where _speed_ is rewarded and highly praised. This is no bad thing in and of itself, companies want to make money and often new features are what makes money. But as a software engineer maintenance takes at least equal priority. So my experience is rooted in a time where reading code was really slow, and 'spaghetti' code was considered extremely harmful a large part because of how much code would have to be read by to understand it. AI really does change the picture here - by being able to trace a dizzying number of call sites and summarising them into a coherent story it can make a formerly un-manageable codebase approachable. 

This is still I think the most amazing thing for me - being able to dispatch an agent to trace the behaviour of a API in another service, or summarise the behaviour of some impenetrable labyrinth of ... unconventional ... code is such a positive change compared to how it used to be. 

So I'm wrestling with the question when doing PR reviews of AI code, namely: _I don't like this code, it is hard to understand and there's about 10x too much to review 'safely'_. 

But -- seriously -- does this still matter? If a developer is creating software by typing a compression of the code they want in an English sentence, and the AI is perfectly capable of compressing the existing codebase down into a form that's changeable, does it matter that I cannot understand the change? 

For me personally am I still of the opinion that yes, coding standards shouldn't change and using AI to write _more_ code is irresponsible at worst, and when compared to using it to the same amount of better code just plain inefficient. But am I right? I actually am doubting myself. 

I think on the 'slow down' side the evidence is 
 - Senior engineers (including myself) authoring code including novice mistakes
 - Noticeably more buggy interactions between systems as more change is put into the two sides or a contract (e.g. mobile vs browser, service-service) 
 - I've noticed less flexibility in adjusting to changing requirements - e.g. because a single engineer can produce an app in no time, an early stage change in product requirements (natural) causes an outsided impact. Generally the _code_ as always is the easiest thing to change, but I've seen much more of my time needing to go into complex database schema refactorings and data migrations than ever before. 

I think the last point is the most fundamental. A code migration has always been 'easy' but the data migration is the challenge. Reducing the application tier coding time probably means even more emphasis on getting the schema right ahead of time. 

I've noticed as well with "spec driven development" that we're possibly moving back towards waterfall style work - when you can get production users in half the time, you're also giving yourself half the time to spot issues with the data model - so you need to be even more sure what you're doing is right before you start.

### Slop grenades

The "slop grenade" (a colossal amount of low quality AI work) is an organisational problem. If you or your colleagues are routinely spamming low quality work and documentation to production, or worse 'helping' your colleagues with PR descriptions that ape a Dickensian sentence structure; toting vertiginous detail, compelling a thesaurus to fathom, then please stop forthwith. If you're a senior you need to have these conversations, yes they're uncomfortable but its your responsibility to use your expertise to guide the team. 

And using AI to reply to your colleagues should not be OK. Forcing a human to argue with a next-token predicator is borderline abusive behaviour.

## Wider trends and "big brain time"

### Productivity and money

I said last year that I'd estimate AI giving engineers a 1-5% productivity increase. I think this is laughably too low, but really for senior engineers I think the productivity gain isn't as high as is claimed. If someone says AI makes them 10x more productive I think that basically means they don't understand productivity statistics. For context in a country like France, the productivity increase for farmers between 1900 (hand tools, horse drawn ploughs) to 1960 (modern fertlisers, tractors) would be something like 8-10x - and globally replicated this transformed human society in the most profound way it has ever changed. Claude code is cool but we're not there yet, sorry. 

The current economic picture seems to be becoming clear - a clear pickup in software companies productivity - good revenue, lower headcount, but at the cost of reduced hiring at the junior level. I'd say this matches my experience exactly - boring time consuming routine coding is now basically fully automated which means I genuinely get an appreciably larger workload done. 

But the thing which interests me is how this is costed for. AI use on a large mature codebase can be really, really expensive i.e. >$1000/month. While its quite easy to get a lot of productivity for a lot less than this I am curious at the executive level how this is being seen. For example a senior engineer in London costs a company at least £10,000 (like $13500 probably) a month to hire. If said engineer spends $12,000/year on AI they have increased their cost to the company by ~10%. So you _need_ a ~10% productivity increase to justify this. Remember that AI power users will go _much_ above this. This is a little catty but my impression of tokenmaxxers believe they are 10x more productive - but actually are they? Certainly code is written _many many_ times faster but does this always translate into _productivity_? My experience using a lot of tokens is that context rot is still a very, very real problem, and that using brain + AI makes it quite hard even to spend this much money. The other thought I had is because AI is still largely a USA product a company in a lower income country like Turkiye pays just as much as a London based engineer - meaning high AI use there is even more of a concern for the bill payers. 

Lastly - I still think valuations for AI adjacent companies are bananas, but equally there's another part of me that thinks maybe some time in the near future the AI models will become fully able to replace human labour, even for expensive office jobs. I think the other factor often overlooked is seeing a person compared to an AI. Lets say it costs an employer £120,000pa to employ a senior - the 120k buys you in the best possible case about 45-46 weeks of work. Unless they get sick, or have a child, or get depressed, or just lose motivation. Then if you don't need them anymore you have to undergo an expensive and time consuming redundancy program, better hope you got everything right, otherwise you're getting sued.

An AI agent seen in the same light is much, much more attractive in comparison. Full productivity always, no sick days, down to the millisecond at-will 'employment'. It is like having an endless supply of gig workers at your beck and call. Uber for the professional classes. I think we need to be vigilante that we don't let this technology erode hard won employment rights.

### Politics

A common theme I've noticed when discussing AI (and technology in general) is that technologists often underestimate the importance of the political system or beliefs of the creators that creates a piece of technology on both itself, and its rollout. While its often the case that technology is influenced more by the natural laws of physics than human ones I feel software is a lot more politised than we might think. Certainly when talking to non-technologists who are critical of AI the recurrent themes are to talk mainly about the people creating the machines and their beliefs than what the AI is doing. 

I think an interesting example of what I mean is dating apps, which have been created overwhelmingly by men, probably mainly because men are more likely to be coders. But its worth thinking about what the these apps show you - massive emphasis on photos, some optional questions to indicate personality. Who is more likely to rate partners mainly based only on looks? Men of course. I hope this isn't cancellable but women tend to take in a broader range of factors when deciding on who they date than men - e.g. personality, humour, career, life plans... What could dating apps have looked like if they were built entirely by a group of women? It seems many complaints about dating apps stem for over-emphasis on looks - men feeling worthless, women feeling objectified. 

While I think the potential for bias in AI prompts has been well covered by progressives its worth taking stock of the air we breathe - the way ChatGPT/Claude etc. talks reflects a highly western, individualist society. While I am inside this culture I can't really critique it but for those outside I wonder if it is jarring? Secondarily the focus of AI to automate office work by the USA - for shareholder capitalist ends - seems to be contrasting with the Chinese focus on future tech like robotics. Its not a surprise Chinese people are more positive about AI than Americans who (clearly rightly) see the technology as a long-term threat to their prosperity and sense of pride at work. 

## Predictions

Strap in, I have literally no idea where this all goes.