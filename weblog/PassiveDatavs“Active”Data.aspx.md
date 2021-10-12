---
title: Passive Data vs “Active” Data
postDate: 2004-12-21T20:27:28.296875-06:00
abstract: In recent SOA related posts I’ve alluded to this, but I wanted to call it out directly. SOA is founded on the principal of passive data.
postStatus: publish
---
21 December 2004

<font face="Times New Roman" color="#000000" size="3">In recent SOA related posts I&#8217;ve alluded to this, but I wanted to call it out directly. SOA is founded on the principal of <i style="mso-bidi-font-style: normal">passive data</i>. Dima Maltsev called this out in a recent comment to a previous blog entry:</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In one of the posts <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:city w:st="on"><st1:place w:st="on">Rockford</st1:place></st1:city> is saying that SOA doesn't address the need of moving data and also the logic associated with that data. I think this is one of the main ideas of SOA and I would rather state it positively: SOA wants you to separate the logic and data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yes, absolutely. SOA is exactly like structured or procedural programming in this regard. All those concepts we studied way back in the COBOL/FORTRAN days while drawing flowcharts and data flow diagrams are <i style="mso-bidi-font-style: normal">exactly</i> what SOA is all about.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Over the past 20-30 years two basic schools of thought have evolved. One ways that data is a passive entity, the other attempts to embed data into active entities (often called objects or components). </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Every now and then someone tries to merge the two concepts, providing a scheme by which sometimes data is passive, while other times it is contained within active entities. Fowlers Data Transfer Objects (DTO) design pattern and my CSLA .NET are examples of recent efforts in this space, though we are hardly alone.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But <i style="mso-bidi-font-style: normal">most</i> people stick with one model or the other. Mixing the models is complex and typically requires extra coding.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Thus, most software is created using a passive data model, or an active entity model alone. And the reality is that the vast majority of software uses a passive data model.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In my speaking I often draw a distinction between <i style="mso-bidi-font-style: normal">data-centric</i> and <i style="mso-bidi-font-style: normal">object-oriented</i> design. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Data-centric design is merely a variation on procedural programming, with the addition of a formalized data container of some sort. In some cases this is as basic as a 2-dimensional array, but in most cases it is a RecordSet, ResultSet, DataSet or some variation on that theme. In .NET it is a DataTable (or a collection of DataTables in a DataSet).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The data-centric model is one where the application goes to the database and retrieves data. The data in the database is passive, and when the application gets it, the data is in a container &#8211; say a DataTable. This container is passive as well.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I hear you arguing already. &#8220;Both the database and DataTable make sure certain columns are numeric!&#8221;, or &#8220;They both make sure the primary key is unique!&#8221;. Sure, that is true. Over the past decade some tiny amount of intelligence has crept into our data containers, but nothing really interesting. Nothing that makes sure the number in the column is a <i style="mso-bidi-font-style: normal">good</i> number &#8211; that it is in the right range, or that it was calculated with the right formula.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Anything along the lines of validation, calculation or manipulation of data occurs <i style="mso-bidi-font-style: normal">outside</i> the data container. That outside entity is the actor, the data container is merely a vessel for passive data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And that&#8217;s OK. That works. Most software is written this way, with the business logic in the UI or a function library (or maybe a rules engine), acting against the data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The problem is that most people don&#8217;t recognize this as procedural programming. Since the DataSet is an object, and your UI form is an object, the assumption is that we&#8217;re object-oriented. Thus we don&#8217;t rigorously apply the lessons learned back in the FORTRAN days about how to organize our code into reusable procedures and organize those procedures into function libraries.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Instead we plop the code into the UI behind button clicks and key press events. Any procedural organization is a token effort, unorganized and informal.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Which is why I favor an active entity approach &#8211; in the form of object-oriented business entity objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In an active entity model, data is never left out &#8220;on its own&#8221; in a passive state. Well, except for when it is in the database, because we&#8217;re stuck using RDBMS databases and the passive data concept is so deeply embedded in that technology it is hopeless&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But once the data comes out of the database it is in an active entity. Again, this is typically an entity object, designed using object-oriented concepts. The primary point here is that the data is never exposed in a raw form. It is never passive. Any external entity using the data can count on the data being validated, calculated and manipulated based on a consistent set of rules that are included <i style="mso-bidi-font-style: normal">with the data</i>.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In this model we avoid putting the logic in the UI. We avoid the need to create procedures and organize them into function libraries like in the days of COBOL. Instead, the logic is part and parcel with the data. They are one.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Most people don&#8217;t take this approach. Historically it has required more coding and more effort. With .NET 1.x some of the overhead is gone, since basic data binding to objects is possible. However, there&#8217;s still the need to map the objects to/from the database and that is certainly extra effort. Also, the data binding isn&#8217;t on a par with that available for the DataSet.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In .NET 2.0 the data binding of objects will be on a par (or better than) binding with a DataSet, so that end of things is improving nicely. The issue of mapping data to/from the database remains, and appears that it will continue to be an issue for some time to come.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In any case, along comes SOA. SOA is all about active entities sending messages to each other. When phrased like that it sounds almost object-oriented, but don&#8217;t be fooled.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The active entities are procedures. Each one is stateless, and each one is defined by a formal contract that specifies the name of the procedure, the parameters it accepts and the results it returns.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Some people will argue that they aren&#8217;t stateless. Indigo, for instance, will allow stateful entities just like DCOM and Remoting to today. But we all know (after nearly 10 years experience with DCOM) that stateful entities don&#8217;t scale and don&#8217;t lead to reliable systems. So if you really <i style="mso-bidi-font-style: normal">want</i> to have an unscalable and unreliable solution then go ahead and use stateful designs. I&#8217;ll be over here in stateless land where things actually work. :-)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The point being, these service-entities are not objects, they are procedures. They accept messages. Message is just another word for data, so they are procedures that accept data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The data is described by a schema &#8211; often an XSD. This schema information has about the same level of &#8220;logic&#8221; as a database or DataSet &#8211; which is to say it is virtually useless. It can make sure a value is numeric, but it can&#8217;t make sure the number is any good.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So Dima is absolutely correct. SOA is all about separating the data (messages) from the logic (procedures aka services).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Is this a good thing? Well that&#8217;s a value judgement.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Did you like how procedural programming worked the first time around? Do you like how data-centric (aka procedural) programming works in VB or Powerbuilder? If so, then you&#8217;ll like SOA &#8211; at least conceptually.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Or do you like how object-oriented programming works? Do you appreciate the consistency and centralized nature of having active entities that wrap your data at all times? Do you feel that the extra effort of doing OO is worth it to gain the benefits? If so, then you&#8217;ll probably balk at SOA.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Note that I say that people happy with procedural programming will <i style="mso-bidi-font-style: normal">conceptually</i> like SOA. That&#8217;s because there&#8217;s always the distributed parallel thing to worry about.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">SOA is inherently a distributed design approach. Yes, you might configure your service-entities to all run on the same machine, or even in the same process. But the <i style="mso-bidi-font-style: normal">point</i> of SOA is that the services are location-transparent. You don&#8217;t <i style="mso-bidi-font-style: normal">know</i> that they are local, and at some point in the future they might not be. Thus you <i style="mso-bidi-font-style: normal">must</i> design under the assumption that each call to a service is bouncing off two satellites as it goes half-way around the planet and back.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">SOA (as described by Pat Helland at least) is also inherently parallel. Calls to services are asynchronous. Your proxy object might simulate a synchronous call, so you don&#8217;t even realize it was async. But a core idea behind SOA is that of transport-transparency. You don&#8217;t know how your message is delivered. Is it via web services? Is it via a queue? Is it via email? You don&#8217;t know. You aren&#8217;t <i style="mso-bidi-font-style: normal">supposed</i> to care.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But even procedural aficionados may not be too keen to program in a distributed parallel environment. The distributed part is complex and can be slow. The parallel part is complex and, well, very complex.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">My predication? Tools like Indigo will avoid the whole parallel part and it will never come to pass. The idea of transport-transparency (or protocol-transparency) will go the way of the dodo before SOA ever becomes truly popular.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The distributed part of the equation can&#8217;t really go away though, so we&#8217;re kind of stuck with that. But we&#8217;ve dealt with that for nearly 10 years now with DCOM, so it isn&#8217;t a big thing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the end, my prediction is that SOA will fade away as people realize that the <i style="mso-bidi-font-style: normal">reality</i> is that we&#8217;ll be using it to do <i style="mso-bidi-font-style: normal">exactly</i> what we did with DCOM, RMI, IIOP and various other RPC technologies.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The really cool ideas &#8211; the ones with the power to be emergent &#8211; are already fading away. They aren&#8217;t included (at least in the forefront) of Indigo, and they&#8217;ll just slip away like a bright and shining dream and we&#8217;ll be left with a cool new way to do RPC.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And RPC is fundamentally a passive data technology. Active entities (procedures) send passive data between them &#8211; often in the form of arrays or more sophisticated containers like a DataSet or perhaps an XML document with an XSD. It is all the same stuff with tiny variations. Like ice cream &#8211; chocolate, vanilla or strawberry, it is all cold and fattening.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">So welcome to the new world, same as the old world.</font>
