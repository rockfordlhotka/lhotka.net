---
title: Unit testing for Windows Phone 7
postDate: 2010-08-10T14:22:31.2355317-05:00
abstract: 
postStatus: publish
---
10 August 2010

I am working on [CSLA 4 for Windows Phone 7](http://www.lhotka.net/weblog/GettingCSLA4ToCompileForWP7.aspx). Of course I want to get all my unit tests (or most of them anyway) running on WP7.

When we created CSLA .NET for Silverlight it was long before Silverlight 2 shipped, and there was no workable unit test framework for Silverlight. Even today, it is tricky to test async methods and features with mstest in SL. Perhaps most importantly however, I wanted to have the same exact unit test code running in .NET and Silverlight – and that’s a level of parity that is hard to achieve.

So Justin created UnitDriven and we donated it to the community through codeplex: http://unitdriven.codeplex.com.

And I have a few hundred unit tests for CSLA that rely on UnitDriven, so it isn’t a trivial thing to think about switching to something else – so it is important that UnitDriven work on WP7 too.

Fortunately Justin was able to get this done in an evening. It turns out that the only major change required was to the UI, because obviously the WP7 form factor is very space constrained compared to a full-size screen.

**The end result is that there’s a preview release of UnitDriven that works on WP7 – you can download it from [codeplex](http://unitdriven.codeplex.com/). **

Most of my CSLA unit tests are passing at this point, which gives us some confidence that UnitDriven is working as expected. There are some UI issues still, especially with long test names and some scrolling issues.

But if you are looking for a way to write unit tests for your WP7 Silverlight code, and especially if you want to use the same unit test code on .NET, Silverlight and WP7, then [UnitDriven](http://unitdriven.codeplex.com/) is something you should consider.
