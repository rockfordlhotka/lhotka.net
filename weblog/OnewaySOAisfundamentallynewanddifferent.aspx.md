---
title: One way SOA is fundamentally new and different
postDate: 2004-10-14T14:12:59.71875-05:00
abstract: I'm listening to Pat Helland speak - and that is always thought provoking
postStatus: publish
---
14 October 2004

<font size="3"><font color="#000000"><font face="Times New Roman">I'm listening to Pat Helland (a serious thought leader in the service-oriented space) speak and it has me seriously thinking.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">I think that one fundamental difference between service-oriented thinking and n-tier is this:<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">We've spent years trying to make distributed systems look and feel like they run in a single memory space on a single computer. But they DON'T. Service-oriented thinking is all about recognizing that we really are running across multiple systems. It is recognition that you can&#8217;t trivialize, abstract or simplify this basic fact. <span style="FONT-SIZE: 12pt; FONT-FAMILY: 'Times New Roman'; mso-fareast-font-family: 'Times New Roman'; mso-ansi-language: EN-US; mso-fareast-language: EN-US; mso-bidi-language: AR-SA">It is acknowledgement that we just can&#8217;t figure it out.</span></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Things like distributed transactions that are designed to make many computers look like one. Heck, CSLA .NET is all about making multiple computers look like a single hosting space for objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And these things only fit into a service-oriented setting <i style="mso-bidi-font-style: normal">inside</i> a service, never between them. The whole point of service-orientation is that services are autonomous and thus don&#8217;t trust each other. Transactions (including work-arounds like optimistic concurrency) are high-trust operations and thus can not exist <i style="mso-bidi-font-style: normal">between</i> autonomous services &#8211; they can only exist inside them.</font>

<o:p><font face="Times New Roman" color="#000000" size="3"><o:p>&nbsp;</o:p></font></o:p>

Personally I don’t think this rules out n-layer or n-tier applications, or n-layer and n-tier *services*. But I do think it reveals how the overall service-oriented may be fundamentally different from n-tier (or OO for that matter).


