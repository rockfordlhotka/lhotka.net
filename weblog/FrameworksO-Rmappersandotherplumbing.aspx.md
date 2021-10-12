---
title: Frameworks, O/R mappers and other plumbing
postDate: 2004-10-01T15:54:40.78125-05:00
abstract: When it comes to frameworks, O/R mappers and other plumbing components: just do it once – build it, buy it, cobble together products to do it. Then get on with building business apps and providing actual value to your organization.
postStatus: publish
---
01 October 2004

<font face="Times New Roman" color="#000000" size="3">It seems that <a href="http://www.TheServerSide.net">TheServerSide.net</a> has a debate going this week about </font>[<font face="Times New Roman" size="3">O/R Mapping</font>](http://www.theserverside.net/news/thread.tss?thread_id=29071)<font face="Times New Roman" color="#000000" size="3">. As part of the discussion, one of the invited debaters made the following comment about CSLA .NET:</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">&#8220;&#8230;everyone just "loves" CSLA, afterall its got every feature imaginable, was created by one of the best "experts", is the subject of books and user groups -- and yes there are code gen templates for it. Now don't get me wrong, I think Rocky is a great speaker and teacher (and great in person too -- I have met him), but I think he would agree that CSLA is an example for teaching how to do something and should not really be the expected to be perfect out-of-the-box -- and its not. I've personally seen a project spend way too much time and effort doing things because they chose this route -- they had to constantly go and add/remove/modify pieces to their chosen framework -- and I've heard many others that have similar problems.&#8221; (<a href="http://www.theserverside.net/news/thread.tss?thread_id=29071#140531">link</a>)</font>

<font face="Times New Roman" color="#000000" size="3">- </font>[<font face="Times New Roman" size="3">Paul Wilson</font>](http://weblogs.asp.net/pwilson/)

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is not the most professionally phrased comment, but this gentleman has previously made similar comments in other forums as well, so I thought I should provide an answer.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I think it is important to note up front that Mr. Wilson </font>[<font face="Times New Roman" size="3">sells an O/R Mapper tool</font>](http://www.ormapper.net/)<font face="Times New Roman" color="#000000" size="3">, and so has some bias. It is also important to note that I have written </font>[<font face="Times New Roman" size="3">numerous books</font>](/publications.aspx)<font face="Times New Roman" color="#000000" size="3"> on distributed object-oriented architecture, and so I have some bias.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">CSLA .NET <i style="mso-bidi-font-style: normal">is</i> intended to be a learning or teaching vehicle. It is often also useful in its own right&nbsp;<span style="FONT-SIZE: 12pt; COLOR: black; FONT-FAMILY: 'Times New Roman'; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">as a development framework</span>.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Different people write different types of books. For instance, Martin Fowler&#8217;s excellent </font>[<font face="Times New Roman" size="3">Patterns of Enterprise Application Architecture</font>](http://www.amazon.com/exec/obidos/tg/detail/-/0321127420)<font face="Times New Roman" color="#000000" size="3"> came out at about the same time as my </font>[<font face="Times New Roman" size="3">.NET Business Objects book</font>](/cslanet)<font face="Times New Roman" color="#000000" size="3">. In many ways he and I are targeting the same demographic, but in different ways. Fowler&#8217;s book stays at a more abstract, conceptual level and teaches from there. My book is more pragmatic and applied, teaching from there.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">As an aside, I find it wonderful how some of the patterns in Fowler&#8217;s book can be found in CSLA .NET. I think this goes to show the power of the design pattern concept &#8211; how patterns emerge in the wild and are documented to help provide a more common language we can all use in future discussions.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But back to books. We need books that give us broad theory and concepts. We also need reference-oriented books that give us basic usage of .NET, C# and VB. And we need books that try to span the gulf between the two. This is where I&#8217;ve tried to live for the most part &#8211; between the theory and reference content. To do this is challenging, and requires that the theory be distilled down into something concrete, but yet rich enough that it isn&#8217;t just more reference material.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The way I&#8217;ve chosen to do this is to pick <i style="mso-bidi-font-style: normal">a way</i> of creating distributed object-oriented applications. Are there other ways? Oh yeah, tons. Are some of them good? Absolutely! Are some of them bad? Again, absolutely. Is CSLA .NET good? It depends.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly I think CSLA .NET and the rest of the content in my business objects books are good for learning how to apply a lot of theory into a complex problem space. I think that many readers use ideas and concepts from my books in conjunction with ideas from Fowler&#8217;s books, </font>[<font face="Times New Roman" size="3">the GoF book</font>](http://www.amazon.com/exec/obidos/tg/detail/-/0201633612)<font face="Times New Roman" color="#000000" size="3"> and lots of other sources.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">A side-effect of writing a book on applied theory is that the theory does actually get applied. This means that the book includes a pretty functional framework that can help build distributed object-oriented applications. This framework, CSLA .NET, can be useful as-is in some scenarios. There&#8217;s a </font>[<font face="Times New Roman" size="3">vibrant online forum</font>](http://groups.msn.com/CSLANET)<font face="Times New Roman" color="#000000" size="3"> for discussion of my books and CSLA .NET where you can find numerous examples where people have applied the framework to help solve their problems.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Many of those people have also modified the framework to better suit their needs or requirements. This is nothing but good. In several cases, modifications made by readers of the books have been applied back into the framework, which is why the framework is currently at version 1.4, where the book described version 1.0.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Does CSLA .NET fit every need? Of course not. No tool meets every need. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is particularly good at creating performant, scalable line-of-business systems that involve a lot of data entry and business rules and relationships. It supports people who build a good object-oriented business entity model, because it provides for virtually unlimited flexibility in translating the object data to arbitrary (relational and/or non-relational) persistence targets (databases, etc).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is not particularly good at creating reporting systems, large batch processing systems or systems that are very data-centric and have little business logic. There&#8217;s also a cost to the data mapping flexibility I mentioned as a benefit &#8211; because with that flexibility comes more work on the developer. If you have either a non-complex data source or you are willing to tie your object model to your data model then CSLA .NET isn&#8217;t ideal because it requires that you do more work. If you want your object model to mirror your data model then use a DataSet, that&#8217;s what it is designed for.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But the real thing to keep in mind, above all else, is this: there is a set of functionality that must exist to build distributed object-oriented enterprise applications. This includes data persistence, UI design support, business logic, organization of layers and tiers, state management and more.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The issues that I address in my business objects books and CSLA .NET <i style="mso-bidi-font-style: normal">are addressed</i> in every enterprise application. Whether formally or informally, whether through reusable or ad-hoc implementations &#8211; everything I address happens in every enterprise app. (And a whole lot more things I <em>don't</em> address are in every enterprise app!!)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The idea that CSLA .NET has &#8220;got every feature imaginable&#8221; seems to imply that it has extra stuff you don&#8217;t need. The fact is that you <i style="mso-bidi-font-style: normal">will</i> address every issue it covers one way or another, plus numerous other issues. You might address them differently that I did, and that&#8217;s great. But you will address them.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You can address them in an ad-hoc manner in each app you write. You can address them through a framework, or you can address them through tools. You might address them through a combination of the above.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But I&#8217;ll say this: the ad-hoc approach is poor. You should opt for a solution that provides reuse and consistency. There are numerous ways to do this, CSLA .NET is one and I imagine that Mr. Wilson&#8217;s O/R mapper tool is another. And there are various commercial frameworks and other O/R mappers out there as well. You have a lot of choices &#8211; which is indicative that this is a healthy segment of our industry.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The fact is that at some point you need to make hard decisions within your organization that move from the theory of design patterns and architecture down to the practical and pragmatic level of code, and you only want to do that once. It is expensive, and it does nothing to solve your actual business needs. All this code that does data persistence, layering, tiering, data binding and whatever else is just plumbing. It is necessary, it is costly, it is time-consuming, and it provides no direct business value.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And be warned &#8211; if you buy or otherwise acquire a framework or tool set (CSLA .NET, O/R mappers, whatever) you will almost certainly need to modify, extend, add or remove bits and pieces to make it fit your needs. If you do this by buying a black-box component of any sort, you&#8217;ll end up extending or modifying <i style="mso-bidi-font-style: normal">around</i> the component, while if you acquire one that includes code you may opt to make the changes inside or outside the component.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Obviously you can acquire a component that does less work for you &#8211; something targeted at a narrow task. In that case you might not need to modify it, but you must face up to the fact that you will need to write all the other stuff that it doesn&#8217;t do. It isn&#8217;t like you can escape the requirement for all this functionality. Every app has it, whether you do it in a reusable form or not is up to you!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So when it comes to frameworks, O/R mappers and all this other plumbing: do it once &#8211; build it, buy it, cobble together products to do it. Whatever suits your fancy. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Then get on with building business apps and providing actual value to your organization.</font>
