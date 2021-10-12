---
title: CSLA Light Prerelease 2 available
postDate: 2008-08-03T23:47:53.354-05:00
abstract: 
postStatus: publish
---
03 August 2008

I've put another prerelease of CSLA Light (CSLA for Silverlight) and CSLA .NET 3.6 online at http://www.lhotka.net/cslalight/download.aspx.

1. Check out the new identity base classes in Csla.Security and Csla.Silverlight.Security - they are pretty darn cool!
2. Check out the new Validator UI control - I think that is really cool!! It won't keep that name, because we're merging the Authorizer functionality directly into that control, so the result will be a consolidated control that does both things - we don't have a name for it yet...
3. I'm pretty sure the ClientContext and GlobalContext work right, but the unit tests don't show that - so I'd recommend viewing that functionality with suspicion.
4. I know some of the security tests don't work. Authentication is still evolving and some of the test apps are lagging a bit behind.


**Please remember, these are very early preview builds. They are not stable. They are not complete. They may or may not work for you. They are not supported.**

We have found, in testing, that Silverlight Beta 2 is not entirely stable. And that WCF in Silverlight is *particularly unstable*. If you run the unit tests in Silverlight you'll probably find what we find - that they randomly fail sometimes. They'll run. They'll fail. Then they'll run again. With no discernable pattern. Quite frustrating, but I guess this is the nature of working on a beta platform.

I have also put the sample app I've been blogging about at http://www.lhotka.net/files/cslalight/SimpleCslaLightAppvb-080803.zip. This sample app shows all the things I've talked about in my Part 1 and Part 2 posts, and I'll be coming out with more posts in the series in the next few days.
