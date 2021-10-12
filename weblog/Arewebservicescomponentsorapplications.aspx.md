---
title: Are web services components or applications?
postDate: 2004-02-11T16:00:44.71875-06:00
abstract: When you create a system with web services, are your web services components or are they standalone applications?
While this might seem like a semantic question, it is actually a very big deal, with a lot of implications in terms of your overall application design, as well as the design of the web services themselves.

postStatus: publish
---
11 February 2004

<font face="Times New Roman" color="#000000" size="3">Applications or Components?</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">When you create a system with web services, are your web services components or are they standalone applications?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">While this might seem like a semantic question, it is actually a very big deal, with a lot of implications in terms of your overall application design, as well as the design of the web services themselves.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I specifically argue that web services are the &#8216;user interface&#8217; to a standalone application. Any other view of web services is flawed and will ultimately lead to a seriously flawed application environment.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Another, simpler, way to put this is that &#8220;a web service is an application, not a tier in an application&#8221;.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Perhaps the key reason this is such an important thing to realize is that almost anyone can use a web service. It isn&#8217;t like we get to pick which other apps will call our web service. Web services are discoverable, and someone, somewhere in our organization (or outside) will discover our web service and will start using it.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If we designed the web service as a tier in our application, we would design it to trust our higher level tiers. If the higher level tier did a bunch of calculations or validations, it would be silly to replicate that functionality in a lower level tier.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">On the other hand, if the web service is a standalone application that merely has an XML interface (as compared to a GUI or HTML interface), it must implement its own calculations and validations. It would be silly for an application <i style="mso-bidi-font-style: normal">not</i> to implement this type of functionality.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So let&#8217;s get back to the component vs application thing. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Components are generally viewed as entities that live within applications. A component provides some functionality that our application can use. But components often have a high degree of trust in the application, and the application certainly has a high degree of trust in the component.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Think of Windows Forms controls, ActiveX controls, encryption libraries, data access (like ADO.NET) and so forth. These are all examples of components, and it is pretty clear that there&#8217;s a high level of trust between them and their hosting applications.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Viewing a web service as a component implies that it is <i style="mso-bidi-font-style: normal">part of</i> an application, rather than actually being an application. This implies a higher level of trust than can be granted to something that is essentially a public API that can be invoked by any application in our organization (or beyond).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Applications, on the other hand, don&#8217;t trust each other. They trade data, they send messages, but they don&#8217;t trust. We&#8217;ve probably all be burned (multiple times) by having too much trust between applications, and we know that it is a bad thing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">By viewing a web service as an application, we can apply full application design principles to its creation. It has a presentation tier (the XML web service itself), a business tier (hopefully a set of business objects, or at least a business DLL), and a data tier (whatever that might be). It is self-contained, doing its own calculation, validation, authentication and so forth.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Other applications can use our web service as a data source, or however they choose. But our web service will be internally consistent and self-protecting. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This ultimately means that the web service will be reliable, useful across multiple applications and in the end will be a good investment in terms of development dollars.</font>


