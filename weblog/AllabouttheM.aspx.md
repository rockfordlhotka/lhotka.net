---
title: All about the &ldquo;M&rdquo;
postDate: 2010-01-13T12:39:46.9048341-06:00
abstract: 
postStatus: publish
---
13 January 2010

I’m often asked whether CSLA .NET supports the MVC, MVP, MVVM or other “M” patterns.

The answer is an absolute YES! Of course it does, because CSLA .NET is all about the “M”.

The “M” in all these patterns stands for Model – the business layer that is supposed to encapsulate all your business logic and the data required for that logic to work.

Since its inception 13+ years ago, CSLA has been primarily focused on helping people build a powerful business layer composed of business domain objects. This implies strong separation of concerns where UI issues are (as much as possible) kept out of the business layer, as are data access concerns.

The various “M” patterns also support separation of concerns. Their perspective is from the UI level, as they are all UI patterns. But at the core of each of them is the idea that the “M” should encapsulate all the business logic, business processing and data required to perform that processing.

Whether you want a Controller-View or a Presenter-View or a View-ViewModel to organize your UI code, in every case you need a clearly separate Model against which the UI will work.

CSLA .NET 3.8 specifically added a bunch of features to simplify the use of MVVM in Silverlight and WPF, but that’s just simplification. MVVM worked fine without those enhancements, it is just a little easier now. Of course you still need an MVVM UI framework, because CSLA isn’t about the UI, it is about the Model.

CSLA .NET 3.8.2 includes a CslaModelBinder for ASP.NET MVC. Again, this simplifies one aspect of using ASP.NET MVC for your UI framework, but it isn’t strictly necessary – it just makes life easier. The same rule applies, CSLA isn’t a UI framework and so does as little as possible at the “V” and “C” level because its focus is all about the “M”.
