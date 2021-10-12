---
title: Yet another boring IaaS offering
postDate: 2013-12-03T11:38:53.8630569-06:00
abstract: 
postStatus: publish
---
03 December 2013

So Google now has an infrastructure as a service (IaaS) offering to compete with Amazon and Microsoft Azure.

[http://news.cnet.com/8301-1023\_3-57614304-93/google-compute-engine-now-ready-for-prime-time/?part=rss&subj=news&tag=title](http://news.cnet.com/8301-1023_3-57614304-93/google-compute-engine-now-ready-for-prime-time/?part=rss&amp;subj=news&amp;tag=title "http://news.cnet.com/8301-1023_3-57614304-93/google-compute-engine-now-ready-for-prime-time/?part=rss&amp;subj=news&amp;tag=title")

From my perspective as a developer this is a big yawn.

IaaS is an IT pro thing – a way of shifting costs from an internal data center (usually capital cost) to an external provider (usually a cash cost). Mostly it is a bunch of accounting details that ultimately result in the same sorts of servers running in a different physical location.

As a developer you don’t really change the way you code just because a server is running onsite, or in a co-location, or in a “cloud”. So who really cares?

IT managers and CFOs care. And really IaaS is fine for an IT manager because they still need pretty much the same size staff to run their servers regardless of where they exist physically. Somebody needs to do server admin, OS upgrades/patches, etc.

Now *platform as a service* (PaaS) like you can get with Windows Azure is FAR more interesting to a developer, but incredibly threatening to IT managers and IT pros.

Azure’s PaaS offering gives developers a higher level of abstraction. Instead of dealing with the OS we get to deal with versions of ASP.NET, and the underlying OS is automatically upgraded/patched (within limits you set).

PaaS *radically* reduces the number of IT staff required to manage and run the “servers” because almost all the work is handled by Azure itself. This can be a massive cost savings to a company due to staff reduction, but you can probably see why IT managers tend to look more at IaaS than PaaS – their “empire” would be in jeopardy by embracing PaaS…

But as a developer, I’d much rather embrace PaaS. IaaS gets me nothing, but PaaS helps me get new compute power provisioned in minutes instead of weeks/months. And it helps minimize the chances that some IT pro will change a low-level configuration on the server, thus breaking my app.

I understand why Google (and Amazon and Microsoft) chase the IaaS market – because there’s money to be had there.

But as a developer who dislikes IT cost accounting and cares little for the size of the IT staff necessary to admin tons of servers, I’d much, much, much rather build my software to run on Azure using the PaaS model.
