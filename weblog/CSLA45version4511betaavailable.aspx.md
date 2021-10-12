---
title: CSLA 4.5 version 4.5.11 beta available
postDate: 2013-02-06T17:36:07.563-06:00
abstract: 
postStatus: publish
---
06 February 2013

I have released a beta of CSLA .NET: version 4.5.11, working toward a final release in a few weeks.

CSLA .NET is an open source software development framework that helps you build a reusable, scalable, and maintainable object-oriented business layer for your applications.

This update includes a few interesting features/changes.

1. Adds support for Windows Phone 8 (WP8) development on the Windows Phone Runtime (WinPRT) platform
2. Simplifies support for ASP.NET MVC 3 and ASP.NET MVC 4, as well as ADO.NET EF 4 and 5 by splitting functionality into separate assemblies and nuget packages
3. Changes the local data portal to have the same behavior as a remote data portal for async calls; specifically this means that the local data portal automatically shifts all async requests onto a background thread from the thread pool
4. Transactional attribute now allows you to set the isolation level
5. Various bug fixes


You can get this prerelease version from nuget in Visual Studio, or you can download the new Wix-based installer from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx).
