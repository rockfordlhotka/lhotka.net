---
title: CSLA .NET 3.7 released with Silverlight 3 support
postDate: 2009-07-21T10:45:08.449-05:00
abstract: 
postStatus: publish
---
21 July 2009

I have released CSLA .NET version 3.7, with support for Silverlight 3.

This is really version 3.6.3, just tweaked slightly to build on Silverlight 3. It turns out that the Visual Studio upgrade wizard didn’t properly update the WCF service reference from Silverlight 2 to Silverlight 3, so I had to rereference the data portal service. I also took this opportunity to fix a couple minor bugs, so check the change logs.

1. If you are a CSLA .NET for Windows user, there’s just one minor change to CslaDataProvider, otherwise 3.7 really is 3.6.3.
2. If you are a CSLA .NET for Silverlight user, there are a couple minor bug fixes in CslaDataProvider and Navigator, and 3.7 builds with Silverlight 3. Otherwise 3.7 is 3.6.3.


In other words, moving from 3.6.3 to 3.7 should be painless.

Downloads are here:

- [CSLA .NET for Windows](http://www.lhotka.net/cslanet/download.aspx)
- [CSLA .NET for Silverlight](http://www.lhotka.net/cslalight/download.aspx)


At this point the 3.6.x branch is frozen, and all future work will occur in 3.7.x until I start working on 4.0 later this year.
