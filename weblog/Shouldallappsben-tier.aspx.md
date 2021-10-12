---
title: Should all apps be n-tier?
postDate: 2005-07-21T16:51:17.062-05:00
abstract: I am often asked whether n-tier (where n>=3) is always the best way to go when building software...
postStatus: publish
---
21 July 2005

<font face="Times New Roman" color="#000000" size="3">I am often asked whether n-tier (where n&gt;=3) is always the best way to go when building software.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course the answer is no. In fact, it is more likely that n-tier is <i style="mso-bidi-font-style: normal">not</i> the way to go!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">By the way, this isn’t the first time I’ve discussed this topic – you’ll find previous blog entries on this blog and an article at </font>[<font face="Times New Roman" size="3">www.devx.com</font>](http://www.devx.com/)<font face="Times New Roman" color="#000000" size="3"> where I’ve covered much of the same material. Of course I also cover it rather a lot in my </font>[<font face="Times New Roman" size="3">Expert VB.NET and C# Business Objects</font>](http://www.lhotka.net/cslanet)<font face="Times New Roman" color="#000000" size="3"> books.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Before proceeding further however, I need to get some terminology out of the way. There’s a huge difference between logical tiers and physical tiers. Personally I typically refer to logical tiers as <i style="mso-bidi-font-style: normal">layers</i> and physical tiers as <i style="mso-bidi-font-style: normal">tiers</i> to avoid confusion.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Logical layers are merely a way of organizing your code. Typical layers include Presentation, Business and Data – the same as the traditional 3-tier model. But when we’re talking about layers, we’re only talking about logical organization of code. In no way is it implied that these layers might run on different computers or in different processes on a single computer or even in a single process on a single computer. <i style="mso-bidi-font-style: normal">All</i> we are doing is discussing a way of organizing a code into a set of layers defined by specific function.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Physical tiers however, are only about where the code runs. Specifically, tiers are places where layers are deployed and where layers run. In other words, tiers are the physical deployment of layers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Why do we layer software? Primarily to gain the benefits of logical organization and grouping of like functionality. Translated to tangible outcomes, logical layers offer reuse, easier maintenance and shorter development cycles. In the final analysis, proper layering of software reduces the cost to develop and maintain an application. Layering is almost always a wonderful thing!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Why do we deploy layers onto multiple tiers? Primarily to obtain a balance between performance, scalability, fault tolerance and security. While there are various other reasons for tiers, these four are the most common. The funny thing is that it is almost impossible to get optimum levels of all four attributes – which is why it is always a trade-off between them.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Tiers imply process and/or network boundaries. A 1-tier model has all the layers running in a single memory space (process) on a single machine. A 2-tier model has some layers running in one memory space and other layers in a different memory space. At the very least these memory spaces exist in different processes on the same computer, but more often they are on different computers. Likewise, a 3-tier model has two boundaries. In general terms, an n-tier model has n-1 boundaries.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Crossing a boundary is expensive. It is on the order of 1000 times slower to make a call across a process boundary <i style="mso-bidi-font-style: normal">on the same machine</i> than to make the same call within the same process. If the call is made across a network it is even slower. It is very obvious then, that the more boundaries you have the slower your application will run, because each boundary has a geometric impact on performance.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Worse, boundaries add raw complexity to software design, network infrastructure, manageability and overall maintainability of a system. In short, the more tiers in an application, the more complexity there is to deal with – which directly increases the cost to build and maintain the application.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This is why, in general terms tiers should be minimized. Tiers are not a good thing, they are a necessary evil required to obtain certain levels of scalability, fault tolerance or security.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">As a good architect you should be dragged kicking and screaming into adding tiers to your system. But there really are good arguments and reasons for adding tiers, and it is important to accommodate them as appropriate.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The reality is that almost all systems today are at least 2-tier. Unless you are using an Access or dBase style database your Data layer is running on its own tier – typically inside of SQL Server, Oracle or DB2. So for the remainder of my discussion I’ll primarily focus on whether you should use a 2-tier or 3-tier model.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If you look at the CSLA .NET architecture from my Expert VB.NET and C# Business Objects books, you’ll immediately note that it has a construct called the DataPortal which is used to abstract the Data Access layer from the Presentation and Business layers. One key feature of the DataPortal is that it allows the Data Access layer to run in-process with the business layer, or in a separate process (or machine) all based on a configuration switch. It was specifically designed to allow an application to switch between a 2-tier or 3-tier model as a configuration option – with no changes required to the actual application code.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But even so, the question remains whether to configure an application for 2 or 3 tiers.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Ultimately this question can only be answered by doing a cost-benefit analysis for your particular environment. You need to weigh the additional complexity and cost of a 3-tier deployment against the benefits it might bring in terms of scalability, fault tolerance or security.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Scalability flows primarily from the ability to get database connection pooling. In CSLA .NET the Data Access layer is entirely responsible for all interaction with the database. This means it opens and closes all database connections. If the Data Access layer for all users is running on a single machine, then all database connections for all users can be pooled. (this does assume of course, that all users employ the same database connection string include the same database user id – that’s a prerequisite for connection pooling in the first place)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The scalability proposition is quite different for web and Windows presentation layers. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In a web presentation the Presentation and Business layers are already running on a shared server (or server farm). So if the Data Access layer also runs on the same machine database connection pooling is automatic. In other words, the web server is an implicit application server, so there’s really no need to have a separate application server just to get scalability in a web setting.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In a Windows presentation the Presentation and Business layers (at least with CSLA .NET) run on the client workstation, taking full advantage of the memory and CPU power available on those machines. If the Data Access layer is also deployed to the client workstations then there’s no real database connection pooling, since each workstation connects to the database directly. By employing an application server to run the Data Access layer all workstations offload that behavior to a central machine where database connection pooling is possible.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The big question with Windows applications is at what point to use an application server to gain scalability. Obviously there’s no objective answer, since it depends on the IO load of the application, pre-existing load on the database server and so forth. In other words it is very dependant on your particular environment and application. This is why the DataPortal concept is so powerful, because it allows you to deploy your application using a 2-tier model at first, and then switch to a 3-tier model later if needed.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">There’s also the possibility that your Windows application will be deployed to a Terminal Services or Citrix server rather than to actual workstations. Obviously this approach totally eliminates the massive scalability benefits of utilizing the memory and CPU of each user’s workstation, but does have the upside of reducing deployment cost and complexity. I am not an expert on either server environment, but it is my understanding that each user session has its own database connection pool on the server, thus acting the same as if each user has their own separate workstation. If this is actually the case, then an application server would have benefit by providing database connection pooling. However, if I’m wrong and all user sessions share database connections across the entire Terminal Services or Citrix server then having an application server would offer no more scalability benefit here than it does in a web application (which is to say virtually none).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Fault tolerance is a bit more complex than scalability. Achieving real fault tolerance requires examination of all failure points that exist between the user and the database – and of course the database itself. And if you want to be complete, you just also consider the user to be a failure point, especially when dealing with workflow, process-oriented or service-oriented systems.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In most cases adding an application server to either a web or Windows environment doesn’t improve fault tolerance. Rather it merely makes it more expensive because you have to make the application server fault tolerant along with the database server, the intervening network infrastructure and any client hardware. In other words, fault tolerance is often less expensive in a 2-tier model than in a 3-tier model.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Security is also a complex topic. For many organizations however, security often comes down to protecting access to the database. From a software perspective this means restricting the code that interacts with the database and providing strict controls over the database connection strings or other database authentication mechanisms.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Security is a case where 3-tier can be beneficial. By putting the Data Access layer onto its own application server tier we isolate all code that interacts with the database onto a central machine (or server farm). More importantly, only that application server needs to have the database connection string or the authentication token needed to access the database server. No web server or Windows workstation needs the keys to the database, which can help improve the overall security of your application.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course we must always remember that switching from 2-tier to 3-tier decreases performance and increases complexity (cost). So any benefits from scalability or security must be sufficient to outweigh these costs. It all comes down to a cost-benefit analysis.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>
