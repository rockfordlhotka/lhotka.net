---
title: StatLight
postDate: 2010-01-11T15:32:31.5283731-06:00
abstract: 
postStatus: publish
---
11 January 2010

If you are doing Silverlight development and have SL unit tests, you should probably take a look at [StatLight](http://statlight.net/).

As CSLA .NET developers are aware, when we created CSLA .NET for Silverlight we had to create our own unit test framework, which we made as a separate open source project called [UnitDriven](http://www.codeplex.com/UnitDriven).

Creating UnitDriven was necessary to allow us to write exactly the same test code to run on both .NET and SL. After all, CSLA .NET works the same (mostly) on both platforms, so having a unified set of tests was critical. And since SL requires a lot of async testing, we also needed a way to implement async unit tests that are exactly the same on .NET and SL.

The big drawback with UnitDriven is that it has an interactive runner – you actually run the SL test app and run the tests by clicking a button. Very nice in some ways, but not useful for continuous integration (CI). And having CI is so very nice…

StatLight works with numerous technologies, including UnitDriven, and enables CI with Silverlight. Absolutely worth checking out!
