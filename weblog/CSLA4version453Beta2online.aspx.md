---
title: CSLA 4 version 4.5.3 Beta 2 online
postDate: 2012-10-04T21:13:38.332859-05:00
abstract: 
postStatus: publish
---
04 October 2012

I have put CSLA 4 version 4.5 beta 2 online as we continue toward the planned final release of version 4.5 on or before Oct 26.

Version 4.5.3 is available via nuget and from the [CSLA download page](http://www.lhotka.net/cslanet/Download.aspx).

The [change log](http://www.lhotka.net/Article.aspx?id=76e23c41-1f45-4c2e-9891-0f1e244dc679) contains a list of all changes. Highlights include:

1. Substantial changes to CslaActionExtender for Windows Forms
2. Substantial (and some breaking) changes to pre- and post-processing methods around the data portal
3. Added the ability to global implement pre- and post-processing handler to server-side data portal to enable logging/tracing and IoC scenarios


At this point we are feature complete, so any releases between now and final release will be bug fixes or stabilization.

Version 4.5 supports the following platforms:

- .NET 4 (with async targeting pack)
- Silverlight 5 (with async targeting pack)
- .NET 4.5
- WinRT


If you are using any of these platforms, please download and test this new release. Here are some notes regarding [upgrading from version 4 to 4.5](http://forums.lhotka.net/forums/t/11624.aspx).
