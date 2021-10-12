---
title: Some thoughts on current trends
postDate: 2016-02-09T15:38:44.069-06:00
abstract: 
postStatus: publish
---
09 February 2016

I’ve been thinking about some of the current trends and hyped terms/concepts lately. On one hand I’m convinced we’re coming out of the inflection point chaos that has consumed our industry over the past several years, and on the other hand any time things start to stabilize the hype-masters come out of the woodwork because there’s money to be made. This isn’t new – see my [SOA, dollar signs and trust boundaries](http://www.lhotka.net/weblog/SOADollarSignsAndTrustBoundaries.aspx) post from 2004…

In this post I’m going to briefly talk about microservices, containers, and devops.

What’s interesting about that 2004 post is that it is one of quite a number of posts I did on service-oriented concepts, and most of my focus at the time was on “pure service-oriented” thinking – which never took off – and which is now known by the newly-trendy term “microservices”.

In other words, this “new” ***microservices*** stuff is just the type of SOA *that we should have been doing for the past decade*. Oops.

As always, when an old idea comes back around under a new name, we owe it to ourselves to ask whether there’s anything different this time that might make the idea more successful than it was last time?

For example, it took us *decades* to get asynchronous programming to become mainstream. We tried over and over again, and it never caught on; until recently there was language/pattern support via things like the async/await keywords in C# and the concept of promises in JavaScript (soon also to be async/await). So what made async programming acessible to the general developer population was a change in languages and tooling.

Given that pure SOA (now microservices) failed to become mainstream in 2004, why do we think it will be successful in 2016? Has anything changed? Do we have new language features or tooling that will make microservice architecture, design, and implementation acessible to the general developer population?

I don’t see it. I don’t see where C# or Java have changed to accomodate service-oriented concepts in any new or novel way. *Other* languages might have done so – F#, Rust, and other niche languages have some neat ideas. But those ideas have yet to work their way into C# or Java, and I think it unrealistic to think that the mainstream business development world is going to shift to these other niche languages (cool though they might be).

I do think there are some interesting *platform*innovations going on, specifically around ***containers***. Yet another trendy hype-laden concept – containers, Docker, etc. Here I’m less skeptical though, because I think containers are in the same vein as Azure PaaS concepts like Web Roles, Web Site, etc. Pre-defined environments in which our code can run without all the complexity of dealing with some random IT person “optimizing a configuration” the night before we go live. That is *never* good, and has been the cause of too many high profile failures in my experience.

The idea that we can build apps that run in a pre-defined, known environment – where the *environment is deployed with the app* is really compelling. To some degree Azure started making this mainstream by providing us with pre-defined and pre-deployed environments that were uniform, consistent, and known. But containers are more flexible, while retaining the key requirement of being pre-defined and consistent.

Personally I expect this container model to transform the way most of us build and think about deploying server-side apps and services over the next few years. Especially (from a Microsoft developer perspective) .NET Core matures on Linux so it runs in Docker, and as Microsoft comes out with Windows containers with comparable predictability to the Linux containers we have today.

Will containers be enough to propel success with microservice architectures all by themselves? I doubt it. I think we need another iteration of language innovation, with a focus on read-only data, message routing patterns, and transparent asynchronicity before microservices will become mainstream.

On the other hand, there is the trendy ***DevOps*** term, which I think is enabled in part by containers. The idea of devops is that we extend what mature/good development shops already do with continuous integration (gated checkins, automatic builds, automated unit test execution) further down the pipeline. So we also automate much of the UX and UAT testing (Magenic has a whole business unit focused on automated QA for example), and automate the creation of “production-ready” deployment assets. Ideally those assets are auto-deployed into a QA or staging environment as a result of each build – or at least they *can* be auto-deployed at the click of a button.

Now those final assets today, if they exist at all, might be in the form of an msi or a deploy-ready website pushed to a git repo. But combining devops with containers means those final assets can be a complete container, ready to be spun up on 1:n servers in QA, staging, or production.

To illustrate this let me share a story. I was recently evaluating [Discourse](http://www.discourse.org/), some very nice, modern forum software. Their only supported deployment mechanism is via Docker containers. They provide a container that you can just host in Docker. So to run a Discourse instance you just need a machine (often a VM – in my case in Azure) where you can install the Docker software. Then you tell Docker to run the Discourse container, and just like that you have a fully realized Discourse instance.

If that wasn’t cool enough (and it was cool!), a couple weeks into my evaluation Discourse came out with a new version. This was visible *in my Discourse admin web page* as an Update button. I clicked that button, causing my Discourse instance to tell the Docker host to download the updated container and to reload the instance using that new container. It was *by far* the most painless upgrade of any software I’ve ever experienced – short of upgrading apps on mobile phones or UWP apps on my Surface.

In other words, devops plus containers has the potential to bring the simplicity of mobile app deployment to server-side environments. Amazing!

Yeah, I’d say it was a lot of hype. Heck I *did* say it was a lot of hype. Then I experienced it first-hand, and it was quite amazing.

So in summary:

- Microservices – mostly hype; I think another iteration of language/tool innovation is required first – give it 5+ years
- Containers – some hype, lots of promise, just coming together now; this will be important over the next 1-3 years
- DevOps – evolution of what good dev shops should already be doing with CI; important now and into the future
- DevOps + Containers – if this comes together like I think it will, I am extremely excited about the future!

