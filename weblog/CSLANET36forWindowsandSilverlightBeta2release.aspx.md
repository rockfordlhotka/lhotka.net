---
title: CSLA .NET 3.6 for Windows and Silverlight Beta 2 release
postDate: 2008-10-21T20:29:29.6443904-05:00
abstract: 
postStatus: publish
---
21 October 2008

I have released Beta 2 of CSLA .NET 3.6, with support for Windows [(download)](http://www.lhotka.net/cslanet/download.aspx) and Silverlight 2.0 [(download)](http://www.lhotka.net/cslalight/download.aspx).

This is an incremental release. Very few issues have been reported or found with Beta 1a, which gives me hope that we're still on track for a final release in the very near future. A lot of hard work by Sergey, Justin, Nermin and other [Magenic](http://www.magenic.com) colleagues have really paid off in the early stability of this version.

CSLA .NET for Silverlight does include one feature change. The Navigator control is now capable of handling a "cold start" scenario, where the user navigates directly to the Silverlight app, specifying a bookmark on the URL. The Navigator control will now immediately help your app navigate to the correct state so the user effectively returns to the page/control/view they'd bookmarked in the first place.

CSLA .NET for Windows also includes one feature change. Nermin is working hard on integrated Visual Studio file and project templates, and an installer project for the templates (and possibly all of CSLA .NET). This work is not yet complete, but Beta 2 has a much more complete set of behaviors than Beta 1.

We believe that this Beta 2 release is very stable. **Please download and use it - on either Windows or Silverlight.** If you have questions/comments or find issues, please [post in the forum](http://forums.lhotka.net).

Also, check out my [DotNet Rocks interview](http://www.dotnetrocks.com/default.aspx?showNum=387) about CSLA .NET for Silverlight.

Finally, for those wondering about the status of the [Expert C# 2008 Business Objects](http://www.apress.com/book/view/9781430210191) book, it is still on track for a December release. Watch http://www.apress.com, as they tell me that they'll be offering an "alpha release" program where you can pre-purchase the book and get early access to chapters in PDF form, and get the paper book when it comes out.

We are also on track for [Expert VB 2008 Business Objects](http://www.apress.com/book/view/1430216387), probably in the February or March timeframe. This is dependent on the 3.6 VB conversion project, which has four [volunteers](http://www.lhotka.net/Article.aspx?area=4&amp;id=bbe426f7-cd06-482f-bfa7-ec5640296562) and is moving along pretty well. I feel pretty confident that this will all come together so the framework and book will both be available to the VB community.

Code well, have fun!
