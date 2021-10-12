---
title: CSLA .NET 3.0 test release #4 available
postDate: 2007-05-04T23:14:37.396968-05:00
abstract: 
postStatus: publish
---
04 May 2007

I have put a test version of CSLA .NET version 3.0 up for download from the [download page](http://www.lhotka.net/cslanet/download.aspx).

This release includes both VB and C# versions of CSLA .NET 3.0, though the WPF support in the VB version has undergone relatively little testing.

The C# ProjectTracker sample is relatively complete, though I'm still chasing down some WPF navigation issues, and may change it over to a Windows-based approach.

The VB ProjectTracker sample isn't as complete, but I've included it in the download nonetheless.

I expect that this is the last pre-release of the CSLA .NET 3.0 framework itself - the next release will be a beta release, and it is my hope to be done with 3.0 by the end of June. If you have the time and inclination, please download the framework and give it a try.

You should be aware that CSLA .NET 3.0 should work just fine on machines with only .NET 2.0, or with .NET 2.0 and 3.0 installed. It also works fine on Orcas Beta 1 (with .NET 2.0, 3.0 and 3.5 installed), though you'll have to upgrade the solution if you try to open it in VS Orcas.

Obviously if you only have .NET 2.0 installed, you can't use WCF or WPF. Attempting to use those features in CSLA .NET will result in compile or runtime errors. However, there are numerous bug fixes and enhancements to other areas of CSLA .NET that may benefit .NET 2.0 users. If you find that CSLA .NET 3.0 doesn't work for you under .NET 2.0 (without .NET 3.0 installed) please let me know so I can address any issues.

I am not aware of any breaking changes from CSLA .NET 2.1, so switching an existing project to use CSLA .NET 3.0 should be straightforward. If it is not, please let me know so I can either address or document any issues.
