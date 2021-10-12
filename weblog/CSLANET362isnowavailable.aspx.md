---
title: CSLA .NET 3.6.2 is now available
postDate: 2009-03-31T16:59:43.1397264-05:00
abstract: 
postStatus: publish
---
31 March 2009

CSLA .NET 3.6.2 is now available for download.

- [CSLA .NET for Windows](http://www.lhotka.net/weblog/ct.ashx?id=543ead80-70bc-4f47-ae63-a8f9e63a94c6&amp;url=http%3a%2f%2fwww.lhotka.net%2fcslanet%2fdownload.aspx)
- [CSLA .NET for Silverlight](http://www.lhotka.net/weblog/ct.ashx?id=543ead80-70bc-4f47-ae63-a8f9e63a94c6&amp;url=http%3a%2f%2fwww.lhotka.net%2fcslalight%2fdownload.aspx)


This is the second point release of CSLA .NET 3.6, and it includes a number of bug fixes, but more importantly there are a number of new features and enhancements based on feedback from users of version 3.6 over the past four months.

Highlights include:
- For both Windows and Silverlight
- New methods on the ObjectFactory base class to better enable creation of a DAL object
- Better support for lazy loaded fields, where an exception is thrown if the field is mis-used accidentally (thus reducing bugs)
- ErrorDialog control for WPF and Silverlight to enable XAML-only handling of exceptions from CslaDataProvider
- CslaDataProvider now has a Saved event to simplify some UI scenarios
- RegisterProperty() now accepts a lambda expression to identify the property name, allowing the compiler to check the name, and avoiding the use of the string literal
- MobileDictionary type, so you can create a dictionary that serializes between Silverlight and .NET
- For Silverlight only
- Better type name resolution, so you can now specify a type by "Namespace.Class, Assembly" without supplying the generic "Version=..." text
- New InventoryDemo sample project (C# only right now - it is a work in progress)
- Code snippets for async factory and data access methods



On a related note, the first segment of my CSLA .NET for Silverlight video series is complete, and I’m nearly done with the web infrastructure for the download site. You can get a summary of the video series content on the [CSLA .NET for Silverlight video download page](http://download.lhotka.net/Default.aspx?t=SLVid01).

Once I get the store and download site complete, you’ll be able to purchase “early adopter'” access to the series – which means you’ll get access to each video segment as soon as it comes online. Look for this in the next couple weeks!
