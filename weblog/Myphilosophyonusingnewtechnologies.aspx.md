---
title: My philosophy on using new technologies
postDate: 2008-04-12T16:11:52.864-05:00
abstract: 
postStatus: publish
---
12 April 2008

Someone on the CSLA .NET discussion forum recently asked what new .NET 3.5 features I used in CSLA .NET 3.5. The poster noted that there are a lot of new features in .NET 3.5, which is true. They also included some .NET 3.0 features as "new", though really those features have now been around for 15 months or so and were addressed in CSLA .NET 3.0. CSLA .NET 3.0 already added support for WCF, WPF and WF, so those technologies had very little impact on CSLA .NET 3.5.

My philosophy is to use new technologies only if they provide value to me and my work. In the case of CSLA .NET this is extended slightly, such that I try to make sure CSLA .NET also *supports* new technologies that might be of value to people who use CSLA .NET.

While .NET 3.5 has a number of new technologies at various levels (UI, data, languages), many of them required no changes to CSLA to support. I like to think this is because I'm always trying to look into the future as I work on CSLA, anticipating at least some of what is coming so I can make the transition smoother. For example, this is why CSLA .NET 2.0 introduced a provider model for the data portal - because I knew WCF was coming in a couple years and I wanted to be ready.

Since CSLA .NET already supported data binding to WPF, Windows Forms and Web Forms, there was no real work to do at the UI level for .NET 3.5. I actually *removed* Csla.Wpf.Validator because WPF now directly supplies that behavior, but I really didn't *add* anything for UI support because it is already there.

Looking forward beyond 3.5, it is possible I'll need to add support for ASP.NET MVC because that technology eschews data binding in favor of other techniques to create the view - but it is too early to know for sure what I'll do in that regard.

Since CSLA .NET has always abstracted the business object concept from the data access technique you choose, it automatically supported LINQ to SQL (and will automatically support ADO.NET EF too). No changes required to do that were required, though I did add Csla.Data.ContextManager to simplify the use of L2S data context objects (as a companion to the new Csla.Data.ConnectionManager for raw ADO.NET connections). And I enhanced Csla.Data.DataMapper to have some more powerful mapping options that may be useful in some L2S or EF scenarios.

LINQ to Objects did require some work. Technically this too was optional, but I felt it was critical, and so there is now "LINQ to CSLA" functionality provided in 3.5 (thanks to my colleague Aaron Erickson). The primary feature of this is creating a synchronized view of a BusinessListBase list when you do a non-projection query, which means you can data bind the results of a non-projection query and allow the user to add/remove items from the query result *and those changes are also reflected in the original list*. As a cool option, LINQ to CSLA also implements indexed queries against lists, so if you are doing many queries against the same list object you should look into this as a performance booster!

So all that's left are some of the language enhancements that exist to support LINQ. And I do use some of them - mostly type inference (which I love). But I didn't go through the entire body of existing code to use the new language features. The risk of breaking functionality that has worked for 6-7 years is *way* too high! I can't see where anyone would choose to take such a risk with a body of code, but especially one like CSLA that is used by thousands of people world-wide.

That means I used some of the new language features in new code, and in code I had to rework anyway. And to be honest, I use those features sparingly and where I thought they helped.

I think trying to force new technologies/concepts/patterns into code is a bad idea. If a given pattern or technology obviously saves code/time/money or has other clear benefits then I use it, but I try never to get attached to some idea such that I force it into places where it doesn't fit with my overall goals.
