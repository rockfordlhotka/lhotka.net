---
title: CSLA 4 version 4.3 beta available
postDate: 2012-02-13T12:45:40.5416317-06:00
abstract: 
postStatus: publish
---
13 February 2012

A beta release of CSLA 4 version 4.3 is now available from here:

http://www.lhotka.net/cslanet/download.aspx

The big change in this beta release is that the Silverlight projects are now bound to Silverlight 5.

I plan to write a document describing how to undo the very few changes required to support Silverlight 5, so if you want to back-port the code for Silverlight 4 you'll be able to do so on your own. This document will be available within the next couple weeks - before the 4.3 release.

The *really* big change came in the previous alpha release: MobileFormatter now allows much more efficient creation of the serialized byte stream, resulting in much smaller amounts of data sent over the network between a Silverlight/Windows Phone client and an app server. This same technology will be used in the WinRT codebase as well.

My plan is to release 4.3 on or before Feb 29.

That will allow us to branch 4.3 in svn so the primary codebase can focus on version 4.5 with support for .NET 4.5 and WinRT.

The 4.3 release will go into maintenance mode - meaning we'll address bugs, but don't plan any more feature changes.
