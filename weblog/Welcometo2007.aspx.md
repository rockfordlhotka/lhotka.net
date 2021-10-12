---
title: Welcome to 2007
postDate: 2007-01-02T09:52:48.0681712-06:00
abstract: 
postStatus: publish
---
02 January 2007

<font size="3"><font color="#000000"><font face="Times New Roman">I you had a good holiday season and enjoyed the end of 2006!<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">For my part, I want to thank everyone who contributed to the </font>[<font face="Times New Roman" color="#800080" size="3">CSLA .NET forums</font>](http://forums.lhotka.net/)<font face="Times New Roman" color="#000000" size="3">, and to the </font>[<font face="Times New Roman" color="#800080" size="3">CSLAcontrib project</font>](http://www.codeplex.com/CSLAcontrib)<font size="3"><font color="#000000"><font face="Times New Roman">. The time and energy you have all put in over the past few months has been a great help to the CSLA .NET community, and I know there are many people out there who are grateful for your efforts!<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Most importantly though, I want to thank all the users of CSLA .NET and everyone who has purchased copies of my books. At the end of the year I received numerous emails thanking me for creating the framework (and I appreciate that), but I seriously want to thank all of you for making this a vibrant community. CSLA .NET is one of the most widely used development frameworks for .NET, and that is because each of you have taken the time to learn and use the framework. Thank you!<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">For me 2006 was a year of change. Starting with CSLA .NET 2.0 I've been viewing CSLA .NET as not just an offshoot of my books, but as a framework in its own right. Of course many people have been treating it that way for years now, but I hope it has been helpful to have me treat point releases a bit more formally over the past number of months.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">This extends to version 2.1, which represents an even larger change for me. With version 2.1 I'm releasing my first self-published ebook to cover the changes. This ebook is not a standalone book, rather it is best thought of as a "sequel" to the 2005 book. However, it is well over 150 pages and covers both the changes to the framework itself, as well as how to use the changes in your application development. The ebook is undergoing technical review. That and the editing process should take 2-3 weeks, so the ebook will be available later this month.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Looking at the rest of 2007 it is clear that I'll be spending a lot of time around .NET 3.0 and 3.5. <o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I'll be merging the </font>[<font face="Times New Roman" color="#800080" size="3">WcfChannel</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=0eec56bb-2a61-47c4-a9ca-f98371db1cad)<font size="3"><font color="#000000"><font face="Times New Roman"> into CSLA .NET itself, as well as implementing support for the DataContract/DataMember concepts. This, possibly coupled with one WPF interface implementation for collections, will comprise CSLA .NET 3.0.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">It is not yet clear to me what changes will occur due to .NET 3.5, but I expect them to be more extensive. Some of the new C#/VB language features, such as extension methods and lambda expressions, have the potential to radically change the way we think about interacting with objects and fields. When you can add arbitrary methods to any type (even sealed types like String) many interesting options become available.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Then there's the impact of LINQ itself, and integration with the ADO.NET Entity Framework in one manner or another. <o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">ADO EF appears, at least on the surface, to be YAORM (yet another ORM). If that continues to be true, then it is a great way to get table data into data entities, but it doesn't <i style="mso-bidi-font-style: normal">really</i> address mapping the data into objects designed around use cases and responsibility. If you search this forum for discussions on nHibernate you'll quickly see how ADO EF might fit into the CSLA .NET worldview just like nHibernate does today: as a powerful replacement for basic ADO.NET and/or the DAAB.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">LINQ is potentially more interesting, yet more challenging. It allows you to run select queries across collections. At first glance you might think this eliminates the need for things like SortedBindingList or FilteredBindingList. I’m not sure that’s true though, because the result of any LINQ query is an IEnumerable&lt;T&gt;. This is <i style="mso-bidi-font-style: normal">the most basic</i> type of list in .NET; so basic that the result must often be converted to a more capable list type.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly when you start thinking about n-level undo this becomes problematic. BusinessBase (BB) and BusinessListBase (BLB) work together to implement the undo capabilities provided by CSLA .NET. Running a LINQ query across a BLB results in an IEnumerable&lt;T&gt;, where T is your BB-derived child type. At this point you’ve lost all n-level undo support, and data binding (Windows Forms, and any WPF grid) won’t work right either.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So at the moment, I’m looking at LINQ being most useful in the Data Access Layer, along with ADO EF, but time will tell.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The point of all this rambling is this: I didn’t rush CSLA .NET 1.0 or 2.0. They came out when I felt I had good understanding of the issues I wanted to address in .NET 1.0 and .20 respectively. And when I felt I had meaningful solutions or answers to those issues. I’m treating .NET 3.5 (and presumably CSLA .NET 3.5) the same way. I won’t rush CSLA .NET to meet an arbitrary deadline, and certainly not to match Microsoft’s release of .NET 3.5 itself. There’s no point coming out with version of CSLA .NET that misses the mark, or that provides poor solutions to key issues.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So in 2007 I’ll most certainly be releasing the version 2.1 ebook and CSLA .NET 3.0 (probably with another small ebook). Given that Microsoft’s vague plans are to have .NET 3.5 out near the end of 2007, I don’t expect CSLA .NET 3.5 to be done until sometime in 2008; but you can expect to see beta versions and/or my experiments around .NET 3.5 as the year goes on.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course I’ll be doing other things beyond CSLA .NET in 2007. I’m lined up to speak at the SD West and VS Live San Francisco conferences in March. I’m speaking in <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:city w:st="on">Denver</st1:city> and <st1:city w:st="on"><st1:place w:st="on">Boulder</st1:place></st1:city> later in January, and I’ll be doing other speaking around the country and/or world as the year goes on. </font>[<font face="Times New Roman" color="#800080" size="3">Click here</font>](http://www.lhotka.net/Presentations.aspx)<font face="Times New Roman" color="#000000" size="3"> for the page where I maintain a list of my current speaking engagements.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To close, thank you all for your support of the CSLA .NET community, and for your kind words over the past many months. I wish you all the best in 2007.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Code well, have fun!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Rocky</font>
