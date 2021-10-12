---
title: Expert 2008 Business Objects, CSLA Light, C# and VB
postDate: 2008-06-23T10:18:31.450816-05:00
abstract: 
postStatus: publish
---
23 June 2008

A couple people have suggested that I might be abandoning VB. Not so!

My first love was Pascal - VAX Pascal actually, which was more like Modula II in many ways. What an awesome language!

My next love was VAX Basic. Now that VB has structured exception handling in .NET, it has finally caught up to where VAX Basic was in the early 90's. No kidding.

Of course after VAX Basic came VB.

And after VB came .NET. I love .NET. I love .NET with VB and C#. C# is just VB with semi-colons, but VB is just C# without semi-colons too. I gave up on the silly language war thing a couple years ago, and am happy to let either or both language live or die by the hand of its users. The language thing was distracting me from truly enjoying .NET.

When it comes to writing books, it is really important to remember that they fund CSLA .NET. As much as I love what I do, I've got kids that will go to college in the (scarily near) future, so I can't work for free. So when I write a book, I can't ignore that C# books outsell VB books around 3:1 (it used to be 2:1, but the market has continued to shift). I still think it is worth writing a VB edition to get that 25% of the market, but you must admit that it makes a lot of sense to go for the 75% first!

It takes several weeks to port a book from one language to the other. The current plan for Expert 2008 Business Objects in C# is October (though I fear that may slip), and with the conversion time and publication schedule constraints, that pushes the VB edition into early 2009. Apress just hasn't put the VB book on their public release list yet, but that doesn't mean I don't plan to do that edition.

When it comes to CSLA Light, I'm doing it in C# because of the 3:1 split, and so again am focusing on C# first.

Whether I do a VB version of the framework or not depends on whether I decide to write a book on the creation and design of CSLA Light. I may or may not. If I don't write a book on the design of the actual framework, I won't port (and then maintain) the framework into a second language.

It is a ridiculous amount of work to maintain CSLA .NET twice, and I really don't like the idea of maintaining CSLA Light twice too. You have no idea how much writing, testing and debugging everything twice slows down progress (and eliminates fun). As wonderful as [Instant C#](http://www.tangiblesoftwaresolutions.com/Product_Details/Instant_CSharp.htm) and [Instant VB](http://www.tangiblesoftwaresolutions.com/Product_Details/Instant_VB.htm)are, the dual effort is a continually increasing barrier to progress.

I might write an ebook on *using* CSLA Light, in which case I'd leave the framework in C#, but create reference apps in both VB and C# so I can do both editions of the ebook. I think this is the most likely scenario. Certainly VB-compatibility has shaped a couple CSLA Light design decisions already - I won't allow a design that precludes the use of VB to build a CSLA Light app.

(The lack of multi-line lambdas and/or anonymous delegates in VB is a real barrier though... Worse even, than the poor way C# handles implementation of interfaces...)

In the end though, like all of us, I need to be where the market is vibrant. Where I can make money from my hard work. Just now, there's more money to be had from C# content and so that takes priority. But there are a lot of people using VB, and (assuming the sales ratio doesn't slip further) in my view it is worth producing content in the VB space as well.
