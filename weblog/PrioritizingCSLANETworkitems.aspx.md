---
title: Prioritizing CSLA .NET work items
postDate: 2009-11-02T10:25:17.6570566-06:00
abstract: 
postStatus: publish
---
02 November 2009

When I sit down to work on CSLA .NET I look at the [wish list](http://www.lhotka.net/cslabugs/), and I tend to order my work based on a few priorities:

1. Is it a bug with no workaround?
2. Will it help a Magenic client/project?
3. Is it fun/interesting/intellectually stimulating to me?
4. Will it help make the lives of a reasonable number of users better?
5. Is it easy (low-hanging fruit)?
6. Does it make CSLA more "complete"? (like the recent MVVM work)


And there are some anti-priorities:

1. Is it boring? Or worse, boring *and time consuming*?
2. Does it increase complexity without amazing payoff in productivity/flexibility?
3. Does it increase my testing/support surface area?
4. Does it focus on "legacy" technologies (now including Windows Forms, Remoting, asmx, Enterprise Services and maybe Web Forms)?
5. Does it solve a problem that's already been solved? (like ORM stuff or UI framework stuff)


These priorities are especially important during point releases, but they certainly factor into major releases (like 4.0) as well. Though the "fun factor" becomes a much bigger priority for major releases, and tactical things like bug fixes or specific Magenic client requirements are usually not as big an issue.

I guess this is one advantage of working on a free framework. Since I’m not directly making money by selling the framework, I can prioritize what I do based on my own intellectual stimulation and fun as much as anything else.
