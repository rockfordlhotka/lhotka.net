---
title: CSLA .NET 3.8 Beta 1 available
postDate: 2009-10-03T23:07:14.9705421-05:00
abstract: 
postStatus: publish
---
03 October 2009

CSLA .NET version 3.8 Beta 1 is now available for download.

- [Download for Windows](http://www.lhotka.net/cslanet/download.aspx)
- [Download for Silverlight](http://www.lhotka.net/cslalight/download.aspx)


Beta 1 brings the WPF PropertyStatus in line with the Silverlight version.

And Beta 1 adds support for the System.ComponentModel.DataAnnotations attributes. Data annotation attributes applied to properties are automatically added as rules using the CSLA .NET validation rules subsystem when ValidationRules.AddAnnotations() is called in your AddBusinessRules() override. If you don’t override AddBusinessRules() the base implementation calls AddAnnotations() on your behalf.

The C# ProjectTracker has been updated to work with 3.8.
