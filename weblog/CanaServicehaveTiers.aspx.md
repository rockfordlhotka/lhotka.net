---
title: Can a Service have Tiers?
postDate: 2005-02-03T23:32:50.484375-06:00
abstract: Coffee after desert and driving in Chicago traffic makes for a brain that won't shut off...
postStatus: publish
---
03 February 2005

<font face="Times New Roman" color="#000000" size="3">One last post on SOA from my coffee-buzzed, Chicago-traffic-addled mind.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Can a Service have Tiers?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly a Service can have layers. Any good software will have layers. In the case of a Service these layers will likely be:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">1.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Interface</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">2.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Business</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">3.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Data access</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">4.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Data management</font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This only makes sense. You’ll organize your message-parsing and XML handling code into the interface layer, which will invoke the business layer to do actual work. The business layer may invoke the Data access layer to get/save data into the Data management (database) layer.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But layers are <i style="mso-bidi-font-style: normal">logical</i> constructs. They are just a way of organizing code so it is maintainable, readable and reusable. Layers say nothing about how the code is deployed – that is the realm of tiers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So the question remains, can a Service be divided into tiers?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I’ll argue yes.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You deploy layers onto different tiers in an effort to get a good trade-off between performance, scalability, fault-tolerance and security. More tiers mean worse performance, but may result in better scalability or security.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If I create a service, I may very well need to deploy it such that I can provide high levels of scalability or security. To do this, I may need to deploy some of my service’s layers onto different tiers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This is no different – absolutely no different – than what we do with web applications. This shouldn’t be a surprise, since a web service is nothing more than a web application that spits out XML instead of HTML. It seems pretty obvious that the rules are the same.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And there are cases where a web application needs to have tiers to scale or to be secure. It follows then that the same is true for web services.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Thus, services can be deployed into multiple tiers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yet the SOA purists would argue that any tier boundary should really be a service boundary. And this is where things get nuts. Because a service boundary implies lack of trust, while a layer boundary implies complete trust. Tiers are merely deployments of layers, so tiers imply complete trust too.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">(By trust here I am not talking about security – I’m talking about data trust. A service must treat any caller – even another service – as an untrusted entity. It must assume that any inbound data breaks rules. If a service <i style="mso-bidi-font-style: normal">does</i> extend trust then it instantly becomes unmaintainable in the long run and you just gave up the primary benefit of SOA.)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So if a tier is really a service boundary, then we’re saying that we have multiple services, one calling the next. But services pretty much always have those four layers I mentioned earlier, so now each “was-tier-now-is-service” will have those layers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Obviously this is a lot more code to write, and a lot of overhead, since the lower-level service (that would have been a tier) can’t trust the higher level one and must replicate much of its validation and possibly other business logic.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To me, at this point, it is patently obvious that the idea of entirely discarding tiers in favor of services is absurd. Rather, a far better view is to suggest that services can have tiers – private, trusting communications between layers, even across the network between the web server hosting the service interface and the application server hosting the data access code.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And of course this ties right back into my previous post for today on remoting. Because it is quite realistic to expect that you’ll use DCOM/ES/COM+ or remoting to do the communication between the web server and application server for this private communication. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">While DCOM might appear very attractive (and is in many cases), it is often not ideal if there’s a firewall between the web server and application server. While it is technically possible to get DCOM to go through a firewall, I gotta say that this one issue is a major driver for people to move to remoting or web services.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And web services might be very attractive (and is in many cases), it is not ideal if you want to use distributed OO concepts in the implementation of your service.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And there we are back at remoting once again as being a perfectly viable option.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course there’s a whole other discussion we could have about whether there’s any value to using any OO design concepts when implementing a service – but that can be a topic for another time.</font>
