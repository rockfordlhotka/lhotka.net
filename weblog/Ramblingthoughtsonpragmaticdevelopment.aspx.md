---
title: Rambling thoughts on pragmatic development
postDate: 2007-01-03T10:40:32.8985152-06:00
abstract: Whether a developer (mis)uses CSLA .NET to create data-centric objects, or follows my advice and creates responsibility-driven objects is really their choice. But either way, I think good support for the RAD capabilities of the environment is key to attaining high levels of productivity when building interactive applications.
postStatus: publish
---
03 January 2007

<font face="Times New Roman" color="#000000" size="3">I recently received an email that included this bit:</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">“You are killing me. I wrote a rather scathing review of your Professional Business Objects with C# on Amazon.com and on my own blog. However, recently I read a transcription of an ARCast with Ron Jacobs where you talked about business objects. I believe I agreed with everything you said. What are you trying to do to me?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I am just a regular shmoe&nbsp;developer, who preaches when listened to about the joys and benefits of OO design for the common business application. I feel too many develop every application like it is just babysitting a database. Every object’s purpose is for the CRUD of data in a table. I have developed great disdain for companies, development teams, and senior developers who perpetuate this problem. I felt Expert C# 2005 Business Object perpetuates this same kind of design, thus the 3 star rating on Amazon for your book.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the ARCast you mentioned a new book coming out. I am hoping it is the book I have been looking for. If I wrote it myself it would be titled something like, “Business Objects in the Real World.” It would address the problems of data-centric design and how some objects truly are just for managing data and others conduct a business need explained by and expert. These two objects would be pretty different and possibly even use a naming convention to explicitly differentiate the two. For example I don’t want my “true” business objects with getters, setters, isDirty flags or anything else that might make them invalid and popping runtime errors when trying to conduct their business.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Anyway, I could ramble on (It’s my nature). However, I just want to drop you a line and say there is a real disconnect between us, but at the same time, I wanted to show everyone at my office what you were saying in your interview. You were backing me up! However, just months ago I was using your writings to explain what is wrong with software development. We seem to be on the same page, or close anyway, but maybe coming to different conclusions. I guess that’s what is bothering me.”</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The following is my response, which I thought I’d share here on my blog because I ended up rambling on more than I’d planned, and I thought it might be interesting/useful to someone:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">I would guess that the disconnect may flow from our experiences during our careers - what we've seen work and not work over time.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">For my part, I've become very pragmatic. The greatest ideas in the world tend to fall flat in real life because people don't get them, or they have too high a complexity or cost barrier to gain their benefit. For a very long time OO itself fit this category. I remember exploring OO concepts in the late 80's and it was all a joke. The costs were ridiculously high, and the benefits entirely theoretical.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Get into the mid-90's and components show up, making some elements of OO actually useful in real life. But even then RAD was so powerful that the productivity barrier/differential between OO and RAD was ridiculously high. I spent untold amounts of time and effort trying to reconcile these two to allow the use of OO and RAD both - but with limited success. The tools and technologies simply didn't support both concepts - at least not without writing your own frameworks for <i style="mso-bidi-font-style: normal">everything</i> and ignoring all the pre-existing (and established) RAD tools in existence.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Fortunately by this time I'd established both good contacts and a good reputation within key Microsoft product teams. Much of the data binding support in .NET (Windows Forms at least) is influenced by my constant pressure to treat objects as peers to recordset/resultset/dataset constructs. I continue to apply this pressure, because things are still not perfect - and with WPF they have temporarily slid backwards somewhat. But I know people on that team too, and I think they'll improve things as time goes on.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">In the meantime Java popularizes the idea of ORM - but solutions exist for only the most basic scenarios - mapping table data into entity objects. While they claim to address the impedance mismatch problem, they really don't, because they aren't mapping into real OO designs, but rather into data-centric object models. Your disdain for today’s ORM tools must be boundless </font><span style="FONT-FAMILY: Wingdings; mso-ascii-font-family: 'Times New Roman'; mso-hansi-font-family: 'Times New Roman'; mso-char-type: symbol; mso-symbol-font-family: Wingdings"><span style="mso-char-type: symbol; mso-symbol-font-family: Wingdings">J</span></span><font face="Times New Roman"> </font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">For better or worse, Microsoft is following that lead in the next version of ADO.NET - and I don't totally blame them; a real solution is complex enough that it is hard to envision, much less implement. However, here too I hold out hope, because the current crop of "ORM" tools are starting to create nice enough entity objects that it may become possible to envision a tool that maps from entity objects to OO objects using a metadata scheme between the two. This is an area I've been spending some time on of late, and I think there's some good potential here.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Through all this, I've been working primarily with mainstream developers (“</font>[<font face="Times New Roman" color="#800080" size="3">Mort</font>](http://www.lhotka.net/weblog/WhoIsMortAnywayAndWhyShouldHeCareAboutVS2005.aspx)<font size="3"><font color="#000000"><font face="Times New Roman">”). Developers who do this as a job, not as an all-consuming passion. Developers who want to go home to their families, their softball games, their <i style="mso-bidi-font-style: normal">real</i> lives. Who don't want to master "patterns" and "philosophies" like Agile or TDD; but rather they just want to do their job with a set of tools that help them do the right thing.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">I embrace that. This makes me diametrically opposed to the worldviews of a number of my peers who would prefer that the tools do less, so as to raise the bar and drive the mainstream developers out of the industry entirely. But that, imo, is silly. I want mainstream developers to have access to frameworks and tools that help guide them toward doing the right thing - even if they don't take the time to understand the philosophy and patterns at work behind the scenes.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I don't remember when I did the ARCast interview, but I was either referring to the 2005 editions of my business objects books which came out in April/May, or to the ebook I'm finishing now, which covers version 2.1 of my CSLA .NET framework. Odds are it is the former, and it isn't the book you are looking for - though you might enjoy Chapter 6.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">In general I think you can take a couple approaches to thinking about objects. <o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">One approach, and I think the right one, is to realize that <i style="mso-bidi-font-style: normal">all</i> objects are behavior-driven and have a single responsibility. Sometimes that responsibility is to merely act as a data container (DTO or entity object). Other times it is to act as a rich binding source that implements validation, authorization and other behaviors necessary to enable the use of RAD tools. Yet other times it is to implement pure, non-interactive business behavior (though this last area is being partially overrun by workflow technologies like WF).<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Another way to think about objects is to say there are different kinds of object, with different design techniques for each. So entity objects are designed quasi-relationally, process objects are designed somewhat like a workflow, etc. I personally think this is a false abstraction that misses the underlying truth, which is that all objects must be designed around responsibility and behavior as they fit into a use case and architecture.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But sticking with the pure responsibility/behavior concept, CSLA .NET helps address a gaping hole. ORM tools (and similar tools) help create entity objects. Workflow is eroding the need for pure process objects. But there remains this need for rich objects that support a RAD development experience for interactive apps. And CSLA .NET helps fill this gap by making it easier for a developer to create objects that implement rich business behaviors and also directly support Windows Forms, Web Forms and WPF interfaces – leveraging the existing RAD capabilities provided by .NET and Visual Studio.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Whether a developer (mis)uses CSLA .NET to create data-centric objects, or follows my advice and creates responsibility-driven objects is really their choice. But either way, I think good support for the RAD capabilities of the environment is key to attaining high levels of productivity when building interactive applications.</font>
