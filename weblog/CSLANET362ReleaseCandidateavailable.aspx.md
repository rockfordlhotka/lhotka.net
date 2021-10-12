---
title: CSLA .NET 3.6.2 Release Candidate available
postDate: 2009-03-22T18:33:41.4246768-05:00
abstract: 
postStatus: publish
---
22 March 2009

I have made CSLA .NET 3.6.2 RC0 available for download.

- [CSLA .NET for Windows](http://www.lhotka.net/cslanet/download.aspx)
- [CSLA .NET for Silverlight](http://www.lhotka.net/cslalight/download.aspx)


Version 3.6.2 includes a number of bug fixes, but more importantly includes a number of new features and enhancements based on feedback from users of version 3.6. Highlights include:
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


Hopefully this is the final test release of 3.6.2, and I am **planning for a final release on March 30 or 31** (before April Fool’s Day :) ). If you are using 3.6.0 or 3.6.1, *please download and test this release* and let me know if you encounter any issues.
