---
title: What I got out of Object Thinking
postDate: 2005-12-01T21:34:11.4375-06:00
abstract: I’ve recommended David West’s Object Thinking book to many people. I really like the book a lot, and think that his underlying message has tremendous value. But the trick with the book is to take the concepts and philosophy and to adapt it into existing tools.
postStatus: publish
---
01 December 2005

<font face="Times New Roman" color="#000000" size="3">I’ve recommended David West’s </font>[<font face="Times New Roman" size="3">Object Thinking</font>](http://www.amazon.com/gp/product/0735619654/qid=1133492508)<font size="3"><font color="#000000"><font face="Times New Roman"> book to many people. I really like the book a lot, and think that his underlying message has tremendous value. But the trick with the Object Thinking book is to take the concepts and philosophy and to adapt it into existing tools.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">David walks through examples assuming a clean slate. No pre-existing framework like .NET or the JDK. No data binding, nothing. And that's good for making his point, but is somewhat silly in the real world. It is hard to imagine ignoring data binding or all the other powerful plumbing built into .NET...<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Likewise, he ignores the value of IDEs. Take away Intellisense and VS becomes pretty crippled. Yet building all objects as collections of field values basically means that they all become Dictionary objects with business rules attached. No more Intellisense or compile-time checking of anything. Ouch!<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">So in my mind the value of Object Thinking isn't in the idea of creating objects at such an incredibly low level that you lose the value of .NET or of VS. <o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Rather it is in the view that objects have a single responsibility. That they are defined by their behaviors, not by their data. It is in the understanding that no class should be overly complex. If it starts to become complex it is because you aren't factoring the behaviors properly, and aren't effectively leveraging collaboration between your objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You could look at CSLA .NET and wonder why I like Object Thinking. After all, CSLA .NET can help you build some very data-centric object designs. But CSLA .NET can also help you build some very behavior-centric object designs too. That’s really your choice!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">From a behavioral perspective, CSLA .NET merely provides (in 2.0) six broad templates:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Editable single objects</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Editable collections of objects</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Readonly single objects</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Readonly collections of objects</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Command objects</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Times New Roman" size="3">Name/value lists</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">All of which tap into a whole set of underlying concepts including data binding, mobile objects and object persistence.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But the goal is to allow a business developer to design a set of objects that have <i style="mso-bidi-font-style: normal">business-specific</i> responsibilities that are better enabled by leveraging this pre-built functionality.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">A Customer object’s responsibility may be to <i style="mso-bidi-font-style: normal">record valid customer data</i>. By inheriting from BusinessBase, the business developer can focus purely on the behaviors necessary to fulfill that responsibility. The object automatically gets data binding, mobile object and object persistence concepts with essentially no effort. The focus is on the business responsibility and behaviors, not on plumbing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But other objects <i style="mso-bidi-font-style: normal">won’t</i> inherit from CSLA .NET. This, I think, is the biggest single hole in how people use my framework. A real business system has many objects that interact with data, true. But collaboration and behavioral OO modeling means that there should be a lot of objects that <i style="mso-bidi-font-style: normal">don’t</i> interact with data. Rather they implement pure behavior!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">These may be following the observer pattern or other design patterns. They may be business rule implementations, or implementations of business algorithms like pricing or taxing. There’s a whole ton of behaviors that often don’t belong in a BusinessBase-derived object, but rather belong in <i style="mso-bidi-font-style: normal">their own</i> object. Then a BusinessBase-derived object will <i style="mso-bidi-font-style: normal">collaborate</i> with these other objects to do its work.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To me that’s the value in West’s book. The philosophy of each object having a single, clear responsibility. Of objects collaborating with other objects to perform complex tasks, without being complex themselves.</font>


