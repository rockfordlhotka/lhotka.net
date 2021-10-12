---
title: nunit to mstest for CSLA .NET 4
postDate: 2009-12-06T21:02:07.2149732-06:00
abstract: 
postStatus: publish
---
06 December 2009

Last week I spent a few hours switching the CSLA .NET for Windows unit/integration tests from nunit to mstest.

This wasn’t terribly hard, because the tests were originally created with the idea of supporting both test frameworks. Of course as different people added tests over several years time inconsistencies crept in, and that’s what I had to address to make this switch.

I didn’t remove the compiler directives for nunit, so it should take relatively little effort to switch back to nunit, but I don’t personally plan to do that.

mstest is now available in all professional versions of Visual Studio 2010, and Microsoft is obviously faster about getting their test framework updated as .NET and Visual Studio change. Looking at http://www.nunit.org there’s no mention of VS10 or .NET 4.0. Yes, I know people have tweaked nunit to work on .NET 4.0, but mstest allows me to eliminate one level of uncertainty from my process.

Besides, there are all these really cool tools and capabilities in VS10, some of which tie into testing and coverage, and this gives me motivation to play with them :)
