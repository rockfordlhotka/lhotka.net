---
title: My C# journey
postDate: 2004-02-22T14:53:56.625-06:00
abstract: Rocky has been writing a C# edition of his popular VB.NET Business Objects book. Because of his long-term relationship with VB and the VB community there are some concerns...
postStatus: publish
---
22 February 2004

The only reason I started this blog was so I'd have a forum for editorializing. I already have my web site ([www.lhotka.net](/)) for formal information about my books, speaking, [CSLA .NET framework](/ArticleIndex.aspx?area=CSLA%20.NET) and so forth. But I didn't have a good place for editorial thoughts (otherwise known as ranting). Thus the blog, and thus this post.

For those who don't know, I'm in the process of writing a C# edition of my [Expert One-on-One VB.NET Business Objects](http://www.apress.com/book/bookDisplay.html?bID=198) book. The C# edition is due out in May 2004. The planned title is [Expert One-on-One C# Business Objects](http://www.apress.com/book/bookDisplay.html?bID=284).

Before I agreed to write this C# edition, I gave a lot of thought to the project. While there's no doubt that both VB.NET and C# are first-class languages in .NET, the fact is that I've been a strong voice for VB over the past many years. What would people think if I went over to the 'dark side' and actually used C#?

I was worried that the VB community would consider that I'd turned my back on them and/or their chosen language. Heck, I was even a bit worried that I'd fall in love with C# - in which case I *might* actually abandon VB. I was also worried that the C# community wouldn't accept the book or the CSLA .NET framework because of my long-term association with VB (which presumably makes me and my work contemptible to some strange fringe of the C-style language community).

The process of writing the C# edition of the book starts with the code. I really can't go far in the prose until the code has been ported to C#, tested and so forth. So at this point I've spent a fair amount of time doing C#. Additionally, publicity about the C# edition of the book has started, so some people in both the VB and C# communities know it is coming. Due to this, I have some answers to my questions.

First off, I have not fallen in love with C#. It is an OK language, and I understand why people like it. It is the first C-style language that is nearly as easy to use and understand as VB. Using C# merely confirms my original belief that the .NET platform represents the victory of the VB mindset. In many ways, C# really is just VB with semi-colons.


> *By way of disclaimer, I've never been a C-style language person. I started with Basic, went to Pascal, wrote a VT100 terminal emulator in C++, did some FORTRAN, some Modula-2, then VAX Basic and finally VB (starting with version 1 on up to VB.NET).*
>
> *That brief bit of C++ was more than enough to convince me that the C-style world view of the time (this was in 1988 or so) was simply wrong. Managing your own resources is silly, unless you are interacting directly with hardware. C/C++ is simply the wrong tool for business software development.*


For the entire life of VB, it has existed in a managed environment, where memory and other resources were taken care of on our behalf. It has also existed in an environment where programmers didn't usually have to worry about the underlying OS, because there was a nice library of components to do the heavy lifting on our behalf.

This is *exactly* the way .NET works. All that has happened, is that the wonderful world of VB has been extended to the rest of the programming languages out there, so even C-style programmers don't have to deal with all that resource management crap. In many ways, the C-style world has finally been brought into the fold.

So, while I've found my experience with C# to be rewarding, from the perspective of learning a new language, my heart still belongs to VB. At the same time, I do see the attraction of C# for people who've spent their lives using C-style languages. It is a hard thing to switch paradigms, and I fully understand why most C-style developers wouldn't want to stretch themselves to learn a whole new linguistic style. It is the same reason most non-C developers don't want to learn C-style languages, but in reverse.

I'll certainly continue to use C# as well as VB. I anticipate writing a Whidbey edition of the Business Objects books - VB first, followed by C#. I also plan to see if I can get CSLA .NET running on [mono](http://www.go-mono.com/) at some point. Since the VB compiler is far behind the C# compiler in mono, obviously C# will be the choice for that little side project.

My other primary concern revolves around the publicity of the C# edition and what that would mean. Thus far I've only heard from the VB community. Some people have expressed concern, while most people have expressed strong support. This blog entry is intended partially to address the concerns I've heard from the VB community about me possibly giving up VB for C#... But I'm not going to abandon VB just when it is going to get really cool again (in Whidbey we get edit-and-continue, and the My namespace - *very* cool stuff!!).

I've also heard from a number of C# developers, and everyone has been supportive. I haven't heard anything from the hard-core fringe groups yet, but I imagine I will once the book is out. That should be entertaining!

But, to reinforce and/or clarify my stance:

1. .NET really is language neutral. I can't see a serious advantage one would gain by using either VB or C# in a CSLA .NET app. It *just doesn't matter* from a functional perspective.
2. I, personally, am not language neutral. I prefer VB. I think it is more readable and intuitive, and thus provides better self-documentation and long-term maintenance. It is also more accessible to new developers - imo.
3. I fully understand that other people are likewise not language neutral. Some prefer C#. That's cool - see point #1 above.


The whole point behind writing the C# edition of the book is to provide people who choose (or are forced) to use C# the same level of access to the material as the VB community. Because there's a lot of both VB and C# developers out there, it only makes sense to have editions of the book in both languages. If some third language were to rise to equal dominance (in terms of market share), I'd probably write an edition in that language as well.

In the end, the book is not about language. It is about distributed architecture and how object-oriented concepts can fit into that distributed world. It is about using the really cool features of the .NET framework like serialization and remoting to do things that used to be really hard in a much easier way.

Ultimately it is about having fun architecting, designing and developing .NET applications. Certainly that's what drives me, and I hope it is what drives anyone who reads and uses the book and the CSLA .NET framework.

Code well, have fun!
