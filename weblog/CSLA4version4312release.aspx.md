---
title: CSLA 4 version 4.3.12 release
postDate: 2012-06-07T17:09:41.9349717-05:00
abstract: 
postStatus: publish
---
07 June 2012

The final release of a CSLA 4 update is now available (version 4.3.12) .

You can get it from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx) or via nuget.

One cool thing with nuget, is that (thanks to work by Johann Hough) the debug symbols are now available on a symbol server. This means you can step through the CSLA code while debugging if desired (and if you deployed CSLA to your project via nuget).

This release is an update to the previous version 4.3 that includes several bug fixes and a few new features. Most notably:

- Fixed a concurrency bug with the data portal
- Fixed a XAML data binding bug with the PropertyInfo control
- Substantial bug fixes and enhancements to the Windows Forms CslaActionExtender control
- Better exception messages when methods/properties can’t be found


There are others as well – see the [change log](http://www.lhotka.net/Article.aspx?id=1c287e08-d428-4c27-b538-d588e3c55775) for details.
