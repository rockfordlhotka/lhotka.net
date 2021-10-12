---
title: CSLA .NET 3.8.0 Beta 3 available
postDate: 2009-10-30T18:07:05.9386582-05:00
abstract: 
postStatus: publish
---
30 October 2009

CSLA .NET 3.8.0 Beta 3 is now available for download

- [Windows download](http://www.lhotka.net/cslanet/download.aspx)
- [Silverlight download](http://www.lhotka.net/cslalight/download.aspx)


Beta 3 includes fixes for some bugs found in Beta 2 (mostly in ViewModelBase and BusyAnimation), and two more significant changes:

- InvokeMethod no longer attempts to manage the attached UI control’s IsEnabled property; this is a breaking change, but was necessary to avoid an otherwise unavoidable memory leak. It wasn’t a good practice anyway, so this implementation is both safer and better.
- There’s a new Csla.Web.Mvc.CslaModelBinder class; it addresses a key issue around the data annotation validation attributes and how their validation information is reported back to the ASP.NET MVC framework. (I know I said Beta 1 was feature-complete, but this was too important to hold back…)


I’ve also continued to update samples, and I think all the C# samples are now updated, as are some of the VB ones. Hopefully I can get the rest of the VB ones updated before final release.

I am still on track to release 3.8.0 in about a week – hopefully Nov 6 or 9.
