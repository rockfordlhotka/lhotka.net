---
title: Where is Service-Oriented Design?
postDate: 2004-09-28T09:54:07.8125-05:00
abstract: There’s lots of talk about Service-Oriented Architecture (SOA), and Service-Oriented Programming-related constructs like web services and SOAP. There’s even a bit of talk about Service-Oriented Analysis. But where’s Service-Oriented Design?
postStatus: publish
---
28 September 2004

<font face="Times New Roman" color="#000000" size="3">There&#8217;s a lot of talk about Service-Oriented Architecture (SOA), and Service-Oriented Programming-related constructs like web services and SOAP. There&#8217;s even a </font>[<font face="Times New Roman" size="3">bit of talk</font>](http://blogs.msdn.com/richardt/archive/2004/08/30/222784.aspx)<font face="Times New Roman" color="#000000" size="3"> about Service-Oriented Analysis. But where&#8217;s the discussion of Service-Oriented Design?</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I am quite convinced that service-orientation (SO) is no less of a force than object-orientation (OO). For over 30 years our understanding OO has been evolving and slowly, ever so slowly, gaining mindshare in the industry. I think we can apply a (slightly modified) Grady Booch OO quote to SO as well:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">&#8220;Let there be no doubt that <b style="mso-bidi-font-weight: normal">service</b>-oriented design is fundamentally different than traditional structured <b style="mso-bidi-font-weight: normal">or object-oriented</b> design approaches: it requires a different way of thinking about decomposition, and it produces software architectures that are largely outside the realm of the structure <b style="mso-bidi-font-weight: normal">or object-oriented</b> design culture.&#8221;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The bits in bold are my alterations/additions to this famous quote.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">OO includes architecture, analysis, design and programming. Understanding and use of all these components is required to make effective use of OO in an enterprise. Precious few organizations ever pull this off. It requires a major culture and skill shift, which is one key reason why OO is still a popular sideline approach rather than the mainstream approach. (The other key reason is lack of tool support for OO design and programming, but that&#8217;s another topic.)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If SO is as big a thing as OO, and I suspect it is, then SO has decades ahead of it on the way to becoming a popular sideline approach for software development. Maybe in that time OO will have become mainstream, but I&#8217;m not holding my breath&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">As an aside, I very much hope that OOA/D/P do become mainstream at some point. After all, we will need to <i style="mso-bidi-font-style: normal">create</i> services, and a service is just an application with an XML interface (vs HTML or GUI). Creating services requires programming in a more conventional sense, and we&#8217;ll end up choosing between data-centric and OO just like today. Personally I really want to see more OO, because I believe it is far superior. But I&#8217;m pragmatic enough to know that it is far more likely that services will be created using the same data-centric (Recordset, DataSet, XML document) mindsets that are prevalent today in Windows and Web applications&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In my wilder dreams I envision a new programming language that is specifically geared around the creation of services. It might be neither data-centric nor OO, but rather would directly include language constructs to represent service-oriented concepts. I know Microsoft is grafting some of these concepts into VB and C# through the WSE and Indigo technologies, but that&#8217;s like prototyping for something that should come later. Perhaps S#? A language with natural expressions for the ideas inherent in SOA/D/P?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In any case, I am convinced that over the next many years we&#8217;ll need to develop SO architecture, analysis, design and programming as disciplines. Processes, techniques and tools will need to be created around all these areas. Perhaps we can do a better job with SO than we did with OO, but that remains to be seen.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But the focus of my question today is this: where is service-oriented design? There&#8217;s lots of talk and debate about service-oriented architecture. There&#8217;s lots of movement around the creation of technologies (like web services, SOAP and the WS-* stuff) to support service-oriented programming. There&#8217;s tiny bits and pieces of discussion about service-oriented analysis. But I have yet to see any serious discussion of service-oriented design.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Service-oriented design is critical. Doing service-oriented <i style="mso-bidi-font-style: normal">programming</i> without service-oriented design is sure to lead to all sorts of unfortunate and unproductive results. Any modern developer knows that you need to translate your architecture into a tactical design for the architecture to be useful. You also know that programming without a design is a sure-fire way to end up with lots of rework and wasted effort.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Service-oriented design isn&#8217;t about the enterprise messaging standards, or about the transport protocols (HTTP, MSMQ, Biztalk, etc.). Nor is it about the application of WS-this or WS-that. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Service-oriented design is about the design of service-based applications. <span style="FONT-SIZE: 12pt; FONT-FAMILY: 'Times New Roman'; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">It is philosophy. </span>It includes the design of services, service clients and other service-related software constructs. It must focus on concepts like </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

- <font face="Times New Roman" color="#000000" size="3">relationships</font>
- <font face="Times New Roman" color="#000000" size="3">encapsulation</font>
- <font face="Times New Roman" color="#000000" size="3">message structures</font>
- <font face="Times New Roman" color="#000000" size="3">data flow</font>
- <font face="Times New Roman" color="#000000" size="3">process flow</font>
- <font face="Times New Roman" color="#000000" size="3">coupling</font>
- <font face="Times New Roman" color="#000000" size="3">cohesion</font>
- <font face="Times New Roman" color="#000000" size="3">decomposition</font>
- <font face="Times New Roman" color="#000000" size="3">functional grouping</font>
- <font face="Times New Roman" color="#000000" size="3">abstraction</font>
- <font face="Times New Roman" color="#000000" size="3">the service interface</font>
- <font face="Times New Roman" color="#000000" size="3">the service implementation</font>
- <font face="Times New Roman" color="#000000" size="3">granularity</font>
- <font face="Times New Roman" color="#000000" size="3">shared context</font>
- <font face="Times New Roman" color="#000000" size="3">and more&#8230;</font>


<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

[<font face="Times New Roman" size="3">Click here</font>](http://c2.com/cgi/wiki?FundamentalFlawsInProceduralDesigns)<font face="Times New Roman" color="#000000" size="3"> for an interesting discussion of procedural vs OO design. I think we need to have a similar discussion around SO design. What is it that makes SO unique and different from procedural/structured and OO design? Intuitively I tend to think that it is unique, but at this point it hasn&#8217;t been fleshed out and so we can&#8217;t have intelligent or objective discussions about <i style="mso-bidi-font-style: normal">how</i> or <i style="mso-bidi-font-style: normal">when</i> it is different.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the end, I think that SO will require a comparable culture and skill shift to OO. In other words, moving to SO from either the procedural/structured or OO worlds will require major cultural and philosophical changes, and substantial retraining and relearning.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Does this mean OOA/D/P are dead? Not on your life. Neither are procedural/structured design or programming. Most software today is built using procedural techniques, mixed with half-hearted OO code. As we move (over the next 30 years) toward SO, you can bet that procedural and OO will be along for the ride as well.</font>
