---
title: CSLA into the future
postDate: 2008-08-20T16:15:50.786-05:00
abstract: 
postStatus: publish
---
20 August 2008

I've been thinking a lot about the future of CSLA and of .NET, and I'd like thoughtful input.

The .NET platform is, for lack of a better word, fragmenting. We have .NET, the .NET client-only framework, .NET Compact Framework, Silverlight and probably others. All of these are ".NET", but they are all different.

CSLA will soon support .NET and Silverlight. It sort of supports the Client-Only Framework now, but it was just pointed out to me that while it works, there are compiler warnings in this scenario.

For the past 6 or so years, I've been maintaining all my code twice, once in VB and once in C#. This has never been fun, and wouldn't have been possible at all without help from my colleague Brant Estes and from the [Instant VB and Instant C#](http://tangiblesoftwaresolutions.com/) tools. Even with this, the reality is that I have to do everything twice, and test everything twice.

(yes, I have a unified set of unit tests, but there's a ton of manual testing around data binding in Web Forms, Windows Forms, WPF and now Silverlight that can't be automated)

But now I'm faced with a truly horrific future scenario. CSLA .NET, CSLA Light, possibly CSLA CF and CSLA Client-Only. Four versions of the framework. Two languages for each version. Fixing a single bug requiring changing and testing 8 implementations.

Clearly that's not realistic. Not only would it eliminate any fun, but it just isn't practical. I doubt it would be practical even if I made CSLA a commercial product...

Of course I can cut the complexity in half by maintaining the framework in only one programming language.

This is a touchy thing of course. I was thinking Modula II, but I can't find a good compiler for .NET... :)

Seriously though, the clear choice would be to maintain the framework in C#, at which point I run the risk of alienating the VB community. You might argue I should maintain the framework in VB, but (for better or worse) that would almost certainly alienate a much bigger constituency.

The really important thing is that the framework would *support both VB and C#*. Regardless of what I do or don't do inside the framework, it can be used by either language (and other languages for that matter) equally well. After all, most of the .NET framework is written in just one language, yet it is used by everyone equally.

Right now CSLA Light is only in C#, though I'm testing in both VB and C# to make sure it supports both equally. I haven't tried, but I imagine you can use it from Ruby or Python too, since both of those languages work in Silverlight too.

Another alternative would be to solicit help from the community. For example, perhaps one or more people would be willing to help keep the VB version of the framework in sync over time. That has its own complications, but might be a worthy solution.

This also ties into my book projects. I'm working on Chapter 16 of 21 for *Expert C# 2008 Business Objects* right now. As with the previous editions, most of the book is focused on the design and creation of the framework itself, with less focus on how to use the framework.

I think a lot of people would actually prefer a book on how to *use the framework*, not caring so much how and why I implemented things internally. And I'd enjoy writing that book (in VB and C# editions). But as it is, I'm looking at 2-3 months of work to get CSLA .NET 3.6 working in VB (which will have to wait until the current book is done), then a couple months to get the *Expert VB 2008 Business Objects* book done. That's 4-5 months where I could write a book on how to use the framework. Or perhaps a series of highly focused ebooks. Or something along that line.

I haven't reached a decision, I'm just thinking long and hard. Thoughtful input is welcome, thanks!
