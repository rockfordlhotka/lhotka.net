---
title: Frameworks have value
postDate: 2017-01-03T10:53:41-06:00
abstract: 
postStatus: publish
---
03 January 2017

We're having a conversation on [Magenic](http://magenic.com)'s internal forum where we're discussing the current JavaScript community reaction to all these frameworks. Some people in the industry are looking at the chaos of frameworks and libraries and deciding to just write everything in vanilla js - eschewing the use of external dependencies.

And I get that, I really do. However, I'm also an advocate of using frameworks - which shouldn't be surprising coming from the author of [CSLA .NET](http://cslanet.com).

Many years ago I spoke at a Java conference (they were trying to expand into the .NET space too).

At lunch I listened to a conversation between some other folks at the table; they were discussing the use of Spring (which was fairly new at the time).

Their conclusion was that although Spring did a ton of useful and powerful things, it was too big/complex and so they'd rather not use it and solve all those problems themselves (the problems solved by Spring).

I see the same thing all the time with CSLA .NET. People look at it and see something that is big and complex, and thing "those problems can't be that hard to solve", so they end up rewriting (usually poorly) large parts of CSLA.

I say "usually poorly" because *their* job isn't to create a well-tested and reusable framework. Their job is to solve some business problem. So they solve some subset of each problem that Spring or CSLA solves in-depth, and then wonder why their resulting app is unreliable, or performs badly, or whatever.

As the author of a widely used OSS framework, *my* job is to create a framework that solves and abstracts away key problems that business developers would otherwise encounter. Because of this, I'm able to solve those problems in a broader and deeper way than a business developer, who's goal is to put as *little* effort into solving the lower level problem, because it is just a distraction from solving the actual business problem.

So yeah, I do understand that some of these frameworks, like Angular, Spring, CSLA .NET, etc. are complex, and they have their own learning curve. But they exist because they solve a bunch of lower level non-business related problems that you will otherwise have to solve yourself. And the time you spend solving those problems provides *zero* business value, and does ultimately add to the long-term maintenance cost of your resulting business software.

There's not a perfect answer here to be sure. But for my part, I like to think that the massive amounts of time and energy spent by framework authors to truly understand solve those hard non-business problems is time well spent, allowing business developers to be more focused on solving the problems they are actually paid to address.
