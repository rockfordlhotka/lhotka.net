---
title: Some thoughts on Windows Azure
postDate: 2008-12-11T18:31:31.9923088-06:00
abstract: 
postStatus: publish
---
11 December 2008

At PDC, Microsoft announced Windows Azure - their Windows platform for cloud computing. There's a lot we don't know about Azure, including the proper way to pronounce the word. But that doesn't stop me from being both impressed and skeptical and about what I *do* know.

In the rest of this post, as I talk about Azure, I'm talking about the "real Azure". One part of Azure is the idea that Microsoft would host my virtual machine in their cloud - but to me that's not overly interesting, because that's already a commodity market (my local ISP does this, Amazon does this - who doesn't do this??). What I do think is interesting is the more abstract Azure platform, where my code runs in a "role" and has access to a limited set of pre-defined resources. This is the Azure that forces the use of a scale-out architecture.

I was impressed by just how much Microsoft was able to show and demo at the PDC. For a fledgling technology that is only partially defined, it was quite amazing to see end-to-end applications built on stage, from the UI to business logic to data storage. That was unexpected and fun to watch.

I am skeptical as to whether anyone will actually care. I think the primary determination about whether people care will be determined by the price point Microsoft sets. But I also think it will be determined by how Microsoft addresses the "lock-in question".

I expect the pricing to end up in one of three basic scenarios:

1. Azure is priced for the Fortune 500 (or 100) - in which case the vast majority of us won't care about it
2. Azure is priced for the small to mid-sized company space (SMB) - in which case quite a lot of us might be interested
3. Azure is priced to be accessible for hosting your blog, or my blog, or http://www.lhotka.net or other small/personal web sites - in which case the vast majority of us may care a lot about it


These aren't entirely mutually exclusive. I think 2 and 3 could both happen, but I think 1 is by itself. Big enterprises have such different needs than people or SMB, and they do business in such different ways compared to most businesses or people, that I suspect we'll see Microsoft either pursue 1 (which I think would be sad) or 2 and maybe 3.

But there's also the lock-in question. If I built my application for Azure, Microsoft has made it very clear that I will not be able to run my app on my servers. If I need to downsize, or scale back, I really can't. Once you go to Azure, you are there permanently. I suspect this will be a major sticking point for many organizations. I've seen quotes by Microsoft people suggesting that we should all factor our applications into "the part we host" and "the part they host". But even assuming we're all willing to go to that work, and introduce that complexity, this still means that part of my app can *never* run anywhere but on Microsoft's servers.

I suspect this lock-in issue will be the biggest single roadblock to adoption for most organizations (assuming reasonable pricing - which I think is a given).

But I must say that even if Microsoft doesn't back down on this. And even if it does block the success of "Windows Azure" as we see it now, that's probably OK.

Why?

Because I think the *biggest benefit* to Azure is one important concept: an abstract runtime.

If you or I write a .NET web app today, what are the odds that we can just throw it on a random Windows Server 200x box and have it work? Pretty darn small. The same is true for apps written for Unix, Linux or any other platform.

The reason apps can't just "run anywhere" is because they are built for a very broad and ill-defined platform, with no consistently defined architecture. Sure *you* might have an architecture. And I might have one too. But they are probably not the same. The resulting applications probably use different parts of the platform, in different ways, with different dependencies, different configuration requirements and so forth. The end result is that a high level of expertise is required to deploy any one of our apps.

This is one reason the "host a virtual machine" model is becoming so popular. I can build my app however I choose. I can get it running on a VM. Then I can deploy the whole darn VM, preconfigured, to some host. This is one solution to the problem, but it is not very elegant, and it is certainly not very efficient.

I think Azure (whether it succeeds or fails) illustrates a different solution to the problem. Azure defines a limited architecture for applications. It isn't a new architecture, and it isn't the simplest architecture. But it is an architecture that is *known to scale*. And Azure basically says "if you want to play, you play my way". None of this random use of platform features. There are few platform features, and they all fit within this narrow architecture that is known to work.

To me, this idea is the real future of the cloud. We need to quit pretending that every application needs a "unique architecture" and realize that there are just a very few architectures that are known to work. And if we pick a good one for most or all apps, we might suffer a little in the short term (to get onto that architecture), but we win in the long run because our apps really *can* run anywhere. At least anywhere that can host that architecture.

Now in reality, it is not just the architecture. It is a runtime and platform and compilers and tools that support that architecture. Which brings us back to Windows Azure as we know it. But even if Azure fails, I suspect we'll see the rise of similar "restricted runtimes". Runtimes that may leverage parts of .NET (or Java or whatever), but disallow the use of large regions of functionality, and disallow the use of native platform features (from Windows, Linux, etc). Runtimes that *force a specific architecture*, and thus ensure that the resulting apps are far more portable than the typical app is today.
