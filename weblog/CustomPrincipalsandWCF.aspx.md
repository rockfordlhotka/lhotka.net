---
title: Custom Principals and WCF
postDate: 2007-08-09T15:28:24.394-05:00
abstract: 
postStatus: publish
---
09 August 2007

I just spent the past few days pulling my hair out trying to get a custom principal to work in WCF.

Google returned all sorts of interesting, but often outdated and/or overly complex results. I kept looking at the techniques people were using, thinking *this can't be so hard!!!*

Well, it turns out that it isn't that hard, but it is *terribly* obscure... Fortunately I was able to get help from various people, including Clemens Vasters, Juval Lowy and (in this case most importantly) Christian Weyer. Even these noted WCF experts provided an array of options rather than a unified, simple answer like I'd expected.

My conclusion: while WCF really is cool as can be, it is also a deep plumbing technology that begs for abstraction for use by "normal" people.

Anyway, as a result of my queries, Christian got one of his colleagues to write the blog post I *wish* I had found a few days ago: [www.leastprivilege.com - Custom Principals and WCF](http://www.leastprivilege.com%20-%20Custom%20Principals%20and%20WCF).

One of my motivations in researching this issue was for the WCF chapter in my upcoming *Using CSLA .NET 3.0* ebook. There's now a comprehensive discussion of the topic in that chapter, starting with the creation and use of X.509 certificates and walking through the whole process of implementing custom authentication and using a custom principal in a WCF service. Dominick's blog post is great, but only covers about a third of the overall solution in the end.

The ebook should be out toward the end of September, for those who are wondering.
