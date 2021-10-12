---
title: Extending the 3-tier conversation to the web
postDate: 2005-07-24T09:47:26.765625-05:00
abstract: Here are some thoughts on 3-tier and the web – a topic I avoided in my previous couple entries
postStatus: publish
---
24 July 2005

<font face="Times New Roman" color="#000000" size="3">Mike has requested my thoughts on 3-tier and the web – a topic I avoided in my previous couple entries (</font>[<font face="Times New Roman" size="3">1</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=efa88d0a-2388-4909-bee1-c9bddb6e9868)<font face="Times New Roman" color="#000000" size="3"> and </font>[<font face="Times New Roman" size="3">2</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=3a057149-f30a-4350-976b-2c4627e6b8f5)<font face="Times New Roman" color="#000000" size="3">) because I don’t find it as interesting as a smart/intelligent client model. But he’s right, the web is widely used and a lot of poor people are stuck building business software in that environment, so here’s the extension of the previous couple entries into the web environment.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">In my view the web server <i style="mso-bidi-font-style: normal">is an application server</i>, pure and simple. Also, in the web world it is impractical to run the Business layer on the client because the client is a very limited environment. This is largely why the web is far less interesting.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To discuss things in the web world I break the “Presentation” layer into two parts – Presentation and UI. This new Presentation layer is purely responsible for display and input to/from the user – it is the stuff that runs on the browser terminal. The UI layer is responsible for all actual user interaction – navigation, etc. It is the stuff that runs on the web server: your aspx pages in .NET.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In web applications most people consciously (or unconsciously) <i style="mso-bidi-font-style: normal">duplicate</i> most validation code into the Presentation layer so they can get it to run in the browser. Thus is expensive to create/maintain, but is an unfortunate evil required to have a half-way decent user experience in the web environment. You <i style="mso-bidi-font-style: normal">must</i> still have that logic in your actual Business layer of course, because you can never trust the browser - it is too easily bypassed (</font>[<font face="Times New Roman" size="3">Greasemonkey</font>](http://greasemonkey.mozdev.org/)<font size="3"><font color="#000000"><font face="Times New Roman"> anyone?). This is just the way it is on the web, and will be until we get browsers that can run complete code solutions in .NET and/or Java (that's sarcasm btw).<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">On the server side, the web server IS an application server. It fills the exact same role of the mainframe or minicomputer over the past 30 years of computing. For "interactive" applications, it is preferable to run the UI layer, Business layer and Data Access layer all on the web server. This is the simplest (and thus cheapest) model, and provides the best performance[1]. It can also provide very good scalability because it is relatively trivial to create a web farm to scale out to many servers. By creating a web farm you also get very good fault tolerance at a low price-point. Using ISA as a reverse proxy above the web farm you can get good security.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In many organizations the reverse proxy idea isn’t acceptable (not being a security expert I can’t say why…) and so they have a policy saying that the web server is never allowed to interact directly with the database server – thus forcing the existence of an application server that at a minimum runs the Data Access layer. Typically this application server is behind a second firewall. While this security approach hurts performance (often by as much as 50%), it is relatively easily achieved with </font>[<font face="Times New Roman" size="3">CSLA .NET</font>](http://www.lhotka.net/cslanet)<font face="Times New Roman" color="#000000" size="3"> or similar architecture/frameworks.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In other situations people prefer to put the Business layer and Data Access layer on the application server behind the second firewall. This means that the web server only runs the UI layer. Any business processing, validation, etc. must be deferred across the network to the application server. This has a much higher impact on performance (in a bad way).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">However, this latter approach <i style="mso-bidi-font-style: normal">can</i> have a positive scalability impact in certain applications. Specifically applications where there’s not much interactive content, but instead there’s a lot of read-only content. Most read-only content (by definition) has no business logic and can often be served directly from the UI layer. In such applications the IO load for the read-only content can be quite enough to keep the web server very busy. By offloading all business processing to an application server overall scalability may be improved.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course this only really works if the interactive (OLTP) portions of the application are quite limited in comparison to the read-only portions.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Also note that this latter approach suffers from the same drawbacks as the <i style="mso-bidi-font-style: normal">thin client</i> model discussed in my </font>[<font face="Times New Roman" size="3">previous post</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=3a057149-f30a-4350-976b-2c4627e6b8f5)<font face="Times New Roman" color="#000000" size="3">. The most notable problem is that you must come up with a way to do non-chatty communication between the UI layer and the Business layer, without compromising either layer. This is historically very difficult to pull off. What usually happens is that the “business objects” in the Business layer require code to externalize their state (data) into a tabular format such as a DataSet so the UI layer can easily use the data. Of course externalizing object state breaks encapsulation unless it is done with great care, so this is an area requiring extra attention. The typical end result are not objects in a real OO sense, but rather are “objects” comprised of a set of atomic, stateless methods. At this point you don’t have objects at all – you have an API.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the case of CSLA .NET, I apply the mobile object model to this environment. I personally believe it makes things better since it gives you the flexibility to run some of your business logic on the web application server and some on the pure application server as appropriate. Since the Business layer is installed on both the web and application servers, your objects can run in either place as needed.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In short, to make a good web app it is almost required that you must compromise the integrity of your layers and duplication some business logic into the Presentation layer. It sucks, but its life in the wild world of the web. If you <i style="mso-bidi-font-style: normal">can</i> put your UI, Business and Data Access layers on the web application server that’s best. If you can’t (typically due to security) then move only the Data Access layer and keep both UI and Business layers on the web application server. Finally, if you <i style="mso-bidi-font-style: normal">must</i> put the Business layer on a separate application server I prefer to use a mobile object model for flexibility, but recognize that a pure API model on the application server will scale higher and is often required for applications with truly large numbers of concurrent users (like 2000+).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">[1] As someone in a previous post indirectly noted, there’s a relationship between performance and scalability. Performance is the response time of the system for a user. Scalability is what happens to performance as the number of users and/or transactions is increased.</font>
