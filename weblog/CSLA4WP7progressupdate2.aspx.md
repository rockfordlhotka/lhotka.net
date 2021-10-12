---
title: CSLA 4 WP7 progress update 2
postDate: 2010-08-10T20:02:49.2052214-05:00
abstract: 
postStatus: publish
---
10 August 2010

I started by getting the CSLA 4 codebase (from Silverlight) to [compile in WP7](http://www.lhotka.net/weblog/GettingCSLA4ToCompileForWP7.aspx).

As an aside – working with WP7 is really a smooth experience. The emulator works quite well, and the debugging experience is comparable to working with Silverlight. I can see where it would be hard to debug/test things requiring touch or other device hardware, but for basic app development the process is quite enjoyable.

Then we got [UnitDriven running in WP7](http://www.lhotka.net/weblog/UnitTestingForWindowsPhone7.aspx) so I could run my unit tests.

Then I spent some quality time fighting with reflection. Over the years, as .NET has evolved alternatives for reflection, CSLA has adopted those alternatives; dynamic methods and now lambda expressions. The specific things CSLA is doing can’t be easily done using the DLR, or I’d consider using that approach.

But WP7 is based on Silverlight 3, which predates the cool stuff in Silverlight 4. That means that the lambda expression concepts used in CSLA 4 wouldn’t build in WP7 – so I basically put TODO comments in their place to get the codebase to compile. Then I went back through and dug up the older 3.x code and tried to just plug it in, replacing the TODO comments.

That turned out to be a little harder than I expected. As part of replacing reflection, we enhanced the functionality of some of the code in CSLA 4, and the 3.x code didn’t handle all the same scenarios. I don’t want my WP7 code to be incompatible with the .NET/SL implementations though, so this basically meant rewriting the 3.x reflection code to support the CSLA 4 functionality.

After a few hours of work all my dynamic method calling unit tests now pass (except for the one that proves that dynamic method invocation is faster than reflection – obviously that one has no meaning in WP7 at the moment). That’s a relief, as it means that essentially all the core functionality of CSLA 4 now works.

With the notable exception of the data portal. It isn’t clear yet what’s failing, but it appears to have something to do with type resolution. I know that Silverlight and .NET don’t work the same in this regard, and I’m beginning to suspect that either I need to revert some other code back to 3.x, or that WP7 doesn’t act the same as Silverlight 3 or 4.

In any case, this is all very encouraging. I am now quite confident that we’ll be able to take CSLA 4 business classes from Silverlight and run them in .NET or on WP7 without change. Just think about building a business class and knowing that it can be used to create Silverlight, ASP.NET MVC, WP7, WPF, WCF, Web Forms, Windows Forms and asmx interfaces! Too cool!!
