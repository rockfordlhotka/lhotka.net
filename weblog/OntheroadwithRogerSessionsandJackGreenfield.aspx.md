---
title: On the road with Roger Sessions and Jack Greenfield
postDate: 2004-06-21T12:11:44.9375-05:00
abstract: Last week I had the privilege to speak at a series of Microsoft Architect Councils alongside Roger Sessions and Jack Greenfield. Roger, Jack and I had some interesting conversations while on the road.
postStatus: publish
---
21 June 2004

<font face="Times New Roman" color="#000000" size="3">Last week I had the privilege to speak at a series of Microsoft Architect Councils alongside Roger Sessions and Jack Greenfield. The cities where we spoke were <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:city w:st="on">Birmingham</st1:city>, <st1:city w:st="on">Tampa</st1:city>, <st1:city w:st="on">Orlando</st1:city> and <st1:city w:st="on"><st1:place w:st="on">Fort Lauderdale</st1:place></st1:city>.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

[<font face="Times New Roman" size="3">Roger Sessions</font>](http://www.objectwatch.com/)<font face="Times New Roman" color="#000000" size="3"> is quite well-known as an expert in architecture. His latest book discusses architecture using a &#8216;software fortress&#8217; metaphor, where applications are a Fortress, accepting input through a Guard and using Envoys to communicate with other applications. I found the metaphor to be very interesting and accurate in many ways. It dovetails very nicely with my viewpoint on most things, including application design, service design and the role of SOA, web services and remoting.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In particular, I think it fits nicely with my view on distributed object-oriented application design. CSLA .NET enables the creation of the code that goes inside one of Roger&#8217;s Fortress constructs &#8211; be that an application or a service. While XML messages pass back and forth between fortresses, inside the fortress we need some way to actually create functionality and implement business features. This is where object-oriented programming comes into play. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And Roger&#8217;s model allows for the use of distributed technologies <i style="mso-bidi-font-style: normal">inside</i> a fortress as well. So where appropriate, it is perfectly realistic to employ distributed object-oriented concepts in such an environment.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

[<font face="Times New Roman" size="3">Jack Greenfield</font>](http://msdn.microsoft.com/architecture)<font face="Times New Roman" color="#000000" size="3"> is a very well-known personality in the patterns space and in the software modeling space. He currently works for Microsoft as an Architect for Enterprise Frameworks and Tools (the Visual Studio Team System product), focusing specifically on modeling tools, including the SOA designer, class designer, etc. Jack comes from Rational and really provides some excellent insight into how both that world and the Microsoft world work. His current focus is on &#8216;industrializing&#8217; the software industry &#8211; moving us to a place where we create software factories rather than creating software directly. Very interesting stuff!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I had a great time discussing various topics with Jack, including whether industrialization of software is actually a good thing. After all, the industrial revolution was not particularly good for the people working in factories. In the long run, it enabled our society to move <i style="mso-bidi-font-style: normal">beyond</i> an industrial economy and then things got better for everyone, but <i style="mso-bidi-font-style: normal">during</i> the industrial period life pretty much sucked for all but an elite few. I think it would be a shame if the industrial metaphor for software included those details&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Jack doesn&#8217;t think this will occur, and I hope he&#8217;s right. I&#8217;m not entirely convinced, but I guess we&#8217;ll see.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The whole things smells a lot like CASE to me, and that ultimately didn&#8217;t work out. It cost corporations a lot of money, and made a lot of money for some vendors and consultants, but ultimately didn&#8217;t work. I asked Jack why he thought the current crop of tools would work where CASE failed. His answer is that we&#8217;ve matured as an industry. Specifically our ability to describe complex systems through metadata has matured, as has our ability to generate code based on that metadata. I guess we&#8217;ll find out one way or the other over the next 5-10 years. If he&#8217;s right, then the stuff he&#8217;s working on will have a far greater impact on software development than web services, SOAP or SOA could ever dream of.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In any case, I do think that the creation of more powerful modeling tools that are more closely linked to our code and actual deployment environment are very compelling. Certainly the designers coming in Team System are version 1.0 products, and will only go so far, but there&#8217;s no doubt in my mind that this type of close-to-the-code designer has a strong future.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course Jack had to fend off critical questions about why the Class Designer (and the others) deviate from UML. I thought he had very good answers for each question, and I personally agree with the direction Microsoft is going. But then again, I am coming from a VB background &#8211; very </font>[<font face="Times New Roman" size="3">pragmatic and focused on getting actual work done</font>](http://www.neward.net/ted/weblog/index.jsp?date=20040608#1086762873763)<font face="Times New Roman" color="#000000" size="3">. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Pure UML may be able to accurately describe .NET code through various arcane notations, but the reality as that most developers will never understand anything that must be described as &#8220;arcane&#8221;&#8230; The more obvious and comprehensible a notation, the better it will serve those of us trying to just build decent software. The whole idea behind academic research is to come up with concepts that can be <i style="mso-bidi-font-style: normal">adapted</i> to the real world and made practical and useful. I think UML fits the academic definition nicely, and the Class Designer is a good shot at adapting it to something that&#8217;s tangibly useful for the majority of .NET developers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


