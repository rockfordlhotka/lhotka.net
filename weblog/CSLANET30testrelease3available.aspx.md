---
title: CSLA .NET 3.0 test release #3 available
postDate: 2007-04-27T21:48:44.5-05:00
abstract: 
postStatus: publish
---
27 April 2007

The third pre-beta test release of CSLA .NET 3.0 is now [available for download](http://www.lhotka.net/cslanet/download.aspx).

This release doesn't include any major changes from the previous release, but does include a set of bug fixes and stabilization.

This release does include an updated ProjectTracker application, which now includes:

- PTWpf - the almost completed WPF UI for ProjectTracker
- PTWorkflow - a simple workflow that makes use of CSLA-style objects in the activities
- WcfPortal - a data portal host for the WCF data portal channel
- PTWcfService - a WCF service interface, much like the older web service interface
- PTWcfServiceClient - a Windows Forms client app for PTWcfService


Plus, of course, all the pre-existing Windows, ASP.NET and web service interfaces and data portal hosts.

This release is only available in C# at the moment. The WCF data portal channel for VB is complete, and is available directly from the [svn repository](http://www.lhotka.net/Article.aspx?id=5987a664-4b44-45a7-bc1d-695610964718). I'll port the remainder of the changes to VB once I'm more confident that they are stable (which should be in the relatively near future).
