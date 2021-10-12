---
title: CSLA .NET 3.8.2 released
postDate: 2010-02-01T11:35:17.171769-06:00
abstract: 
postStatus: publish
---
01 February 2010

CSLA .NET 3.8.2 is now available for Windows and Silverlight

- [Download for Windows](http://www.lhotka.net/cslanet/download.aspx)
- [Download for Silverlight](http://www.lhotka.net/cslalight/download.aspx)


This is a bug-fix release, and has been in beta for several months.

There is only one real functional (and breaking) change, which affects only people building WPF or Silverlight applications and using the design-time data support built into the data portal. This feature has been disabled in 3.8.2 because there’s an issue in WPF (and possibly Silverlight) where detecting design time vs runtime in a high volume runtime scenario would cause a Win32 exception in the .NET runtime.

Since Visual Studio 2010 and .NET 4.0 have a different way of handling design time data, this was going to change anyway; but making this change now helps avoid this WPF runtime issue, and so was important.
