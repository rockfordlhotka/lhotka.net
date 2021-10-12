---
title: CSLA .NET 3.6.3 for .NET 2.0
postDate: 2009-08-13T11:33:45.823235-05:00
abstract: 
postStatus: publish
---
13 August 2009

CSLA .NET 3.6 normally requires .NET 3.5 SP1. However, if you are using Visual Studio 2008 it is possible (with some work and a third party LINQ library) to get CSLA .NET 3.6 running on .NET 2.0 SP1. Jonny Bekkum has done just that, and has contributed the results of his efforts to the community - thank you Jonny!

The result is a large subset of version 3.6.3 that builds and runs on .NET 2.0 SP1, eliminating the need for .NET 3.5 SP1 (though adding the need for [LINQbridge](http://www.albahari.com/nutshell/linqbridge.aspx), a third-party component).

You get to use the most of the new features in CSLA .NET, including:

1. Managed properties in **BusinessBase**, **ReadOnlyBase** and **CommandBase** that reduces the number of lines required to declare a property.
2. **PropertyInfo** type for less hardcoding of property names in your code.
3. **FieldManager** and **DataPortal** enhancements, including the asynchronous DataPortal and Child\_XYZ mehthods.
4. **ObjectFactory** for separation of BO and DAL
5. **CslaActionExtender** reduces the amount of code behind required in Windows Forms
6. Reflection enhancements (**MethodCaller**) for dynamic calls
7. An easier upgrade path to CSLA .NET 3.7 and Silverlight
8. and a lot more ….


Jonny has not only got the CSLA .NET framework running on .NET 2.0, but he’s got unit tests and samples! This is an amazing contribution to the community.

You can download this version from http://www.lhotka.net/cslanet/N2.aspx.
