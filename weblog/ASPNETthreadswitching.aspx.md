---
title: ASP.NET thread switching
postDate: 2006-01-17T14:48:29.375-06:00
abstract: A blog comment recently made me aware that ASP.NET can switch your thread during a page's processing. This scary thought lead to further research - here are my findings.
postStatus: publish
---
17 January 2006

<font face="Times New Roman" color="#000000" size="3">In a recent entry there was a comment pointing to </font>[<font face="Times New Roman" size="3">this article</font>](http://piers7.blogspot.com/2005/11/threadstatic-callcontext-and_02.html)<font face="Times New Roman" color="#000000" size="3">, which discusses the way ASP.NET uses threads – a fact that has serious ramifications on software design.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It made me do some serious thinking/research, because CSLA .NET uses various elements of the Thread object, including the CurrentPrincipal, thread-local storage and (in 2.0) the culture properties. My fear was that if the thread can switch “randomly” during page processing, then how can you count on any of these elements from the Thread object?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3"><a href="http://weblogs.asp.net/scottgu/">Scott Guthrie</a> from Microsoft clarified this for me on a couple key points.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">First, ASP.NET doesn’t change your thread at “random” or “without warning” (phrases I’d used in describing my worries). It changes it only in a clearly defined scenario. Specifically, when your thread performs an async IO operation. Scott points out that this is perhaps most common in a page that takes advantage of the new async page capability, or within a HttpModule that uses any async IO.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In other words, <i style="mso-bidi-font-style: normal">normal</i> web pages really aren’t subject to this issue at all. It only occurs in relatively advanced scenarios. And you, as the developer, should know darn well when you invoke an async operation; thus you know when you open yourself up for thread switching.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Still, I wanted to make sure the Business Objects book didn’t go down a bad path with the Thread object. But Scott clarified further.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">ASP.NET ensures that, even if they switch your thread, the CurrentPrincipal and culture properties from the original thread carry forward to the new thread. This is automatic, and you don’t need to worry about losing those values. Whew!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman"><i style="mso-bidi-font-style: normal">However</i>, thread-local storage doesn’t carry forward. If you use that feature of the Thread object in ASP.NET code you could be in trouble. This did cause me to rework some code in the book and in CSLA .NET. Specifically CSLA .NET 2.0 now detects whether it is running in ASP.NET or not and uses either thread-local storage or HttpContext.Current.Items to maintain its context data.</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I also went the rest of the way and created a Csla.ApplicationContext.User property that gets and sets the user’s principal on either the Thread or HttpContext based on whether the code is running in ASP.NET or not. This allows you to write code in your UI and objects and other libraries without worrying about whether it might run inside our outside ASP.NET at some point. </font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Certainly for mobile business objects this is very important! They can (and often do) run in both a smart client and ASP.NET environment within the same application.</font>
