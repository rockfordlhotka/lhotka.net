---
title: Serious challenge for unit testing in Silverlight
postDate: 2008-07-17T23:44:51.754-05:00
abstract: 
postStatus: publish
---
17 July 2008

If you've tried to do any unit testing in Silverlight, you may have run into an interesting issue. Many times, unit tests *expect* exceptions. Tests are written to ensure that an exception occurs as expected. That's a standard concept in most unit testing frameworks for .NET.

In Silverlight, there's an "expected CLR behavior" where the debugger will break on exceptions that are actually handled by user code - treating them like they *aren't handled*. See this thread for some more detail:

http://silverlight.net/forums/p/20678/72377.aspx#72377

The result of this, is that you have to employ some ugly workarounds, or you need to press F5 for each of your tests where you expect an exception.

We're running into this issue in a big way with CSLA Light (CSLA .NET for Silverlight), because we're creating lots and lots of unit tests, and a fair number of them are testing to make sure exceptions occur when we expect them.

Of course our unit testing framework ([UnitDriven](http://www.codeplex.com/UnitDriven)) uses reflection to run each test method - just like MSTest or nunit - and so even though we *are handling the exception in user code* the debugger insists on breaking in the test methods themselves where the exceptions occur.

Again, there are workarounds. They prevent you from using the debugger to walk through your tests - but at least they exist. The whole thing is really sad though - given that this is apparently *intended behavior*.
