---
title: VB <-> C# conversions
postDate: 2006-08-01T14:43:49.7833312-05:00
abstract: I've long been skeptical of language conversion tools - but I think I'm changing my tune.
postStatus: publish
---
01 August 2006

Maintaining CSLA .NET, along with the ProjectTracker sample app, in both VB and C# is challenging. I've blogged before about how tedious it is converting C# to VB or visa versa, and how it slows down progress on the framework.

For CSLA .NET 2.0 I was fortunate enough to have the help of Brant Estes from [Magenic](http://www.magenic.com), who put in amazing time and effort to keep the C# code in sync with the VB code through the development and writing process. There was no way I'd have completed the books and framework on schedule without his help!

But recently I've been playing with a set of tools from [Tangible Software Solutions](http://www.tangiblesoftwaresolutions.com/): Instant VB and Instant C#. By way of disclaimer, I got free licenses to these tools thanks to Tangible, and that's why I've been using them. But having used them, I would suggest that they are certainly worth the cost for anyone who needs to convert code one way or the other.

I have been very skeptical of language conversion tools. By and large the results don't look "right". Convert VB to C# and you get working code, but not the kind of code you'd write by hand. It is even worse when converting C# to VB - the results look like C# without the semicolons, and don't resemble *real* VB code hardly at all...

Now I'm not ready to say that Instant VB/C# are perfect, but they are pretty darn good. Better still, I have been providing feedback to Tangible about what I wish was different, and the speed at which they have responded by improving the tools is excellent! Seriously, I think they've given me 2-3 new builds just in the past couple weeks - each one making my life easier.

I'm using the tools in per-file mode, translating individual CSLA .NET source files from C# to VB and from VB to C#. The VB to C# conversions are quite good, and there are only a couple things I'm having to do to the resulting code (clean up the using (Imports) statements, and rename instance variables because I use a 'm' prefix in VB and a '\_' prefix in C#).

The C# to VB isn't quite as smooth yet, but it is getting rapidly better. Tangible is working on an enhancement to translate several common string and type conversion patterns into VB equivalents (Len(), CInt(), etc.) I believe that'll be an option, so if you prefer the C# approach even in your VB code you don't need to worry. Once that is working, I expect to be pretty happy. Even so, I'll need to change instance variables because of my choice of different prefixes - but that's really my issue :)

The thing is, the time savings for me is tremendous. But what makes me write this blog entry is the fact that the resulting code really does look like the kind of code you'd write by hand - and for me that's the true test.
