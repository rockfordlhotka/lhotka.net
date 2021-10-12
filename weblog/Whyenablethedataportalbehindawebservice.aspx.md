---
title: Why enable the data portal behind a web service?
postDate: 2008-01-24T08:01:56.6517584-06:00
abstract: 
postStatus: publish
---
24 January 2008

I reader recently sent me an email asking why the PTWebService project in the CSLA .NET ProjectTracker reference app has support for using the data portal to talk to an application server. His understanding was that web services were end points, and that they should just talk to the database directly. Here's my answer:

A web service is just like any regular web application. The only meaningful difference is that it exposes XML instead of HTML.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

<o:p>&nbsp;</o:p>

Web applications often need to talk to application servers. While you are correct – it is ideal to build web apps in a 2-tier model, there are valid reasons (mostly around security) why organizations choose to build them using a 3-tier model.<o:p></o:p>

<o:p>&nbsp;</o:p>

The most common scenario (probably used by 40% of all organizations) is to put a second firewall between the web server and any internal servers. The web server is then never allowed to talk to the database directly (for security reasons), and instead is required to talk through that second firewall to an app server, which talks to the database.<o:p></o:p>

<o:p>&nbsp;</o:p>

The data portal in CSLA .NET helps address this issue, by allowing a web application to talk to an app server using several possible technologies. Since different organizations allow different technologies to penetrate that second firewall this flexibility is important.<o:p></o:p>

<o:p>&nbsp;</o:p>

Additionally, the data portal exists for other scenarios, like Windows Forms or WPF applications. It would be impractical for me to create different versions of CSLA for different types of application interface. In fact that would defeat the whole point of the framework – which is to provide a consistent and unified environment for building business layers that support all valid interface types (Windows, Web, WPF, Workflow, web service, WCF service, console, etc).
