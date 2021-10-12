---
title: CSLA Light preview release
postDate: 2008-07-15T19:40:52.638288-05:00
abstract: 
postStatus: publish
---
15 July 2008

I have put a *very* early preview release of CSLA Light and CSLA .NET 3.6 online at http://www.lhotka.net/cslalight/download.aspx.

There is no sample app at this point, so you'll have to look at the unit tests in cslalighttest and cslatest to figure out how to use the various features.

Obviously this is *very* early code, but it is healthy to release early and often, so here we go :)

One side-effect of our work with CSLA Light is that we discovered that testing asynchronous methods is really hard with nunit and MSTest, and impossible with the Silverlight unit test framework provided by Microsoft. And yet in Silverlight, async methods are commonly required, and for parity a number of async features are now also in CSLA .NET. And we need to have unit tests for them.

To address this issue, we ended up creating our own Silverlight unit testing framework, and an add-on framework for nunit or MSTest. This allows us to write a common set of test code that runs in both Silverlight and .NET so we can test both, and establish that we have parity between them.

Earier today, Justin split this testing framework out of CSLA and we put it up on CodePlex, calling it [UnitDriven](http://www.codeplex.com/UnitDriven). The [CSLA Light project](http://www.lhotka.net/cslalight)and [Magenic](http://www.magenic.com) are donating the code to the community as an open-source project, because it can be used to build async unit tests for any app, not just for CSLA Light.
