---
title: Services, Objects and People, Oh my!
postDate: 2004-05-29T21:53:54.890625-05:00
abstract: Where do human beings fit into an SOA world? Rocky ruminates on this topic through a Tech Ed induced haze.
postStatus: publish
---
29 May 2004

<font face="Times New Roman" color="#000000" size="3">This week at Tech Ed in <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:city w:st="on"><st1:place w:st="on">San Diego</st1:place></st1:city> I got an opportunity to talk to <a href="http://www.chappellassoc.com/">David Chappell </a>and trade some thoughts about SOA, Biztalk and Web services. I always enjoy getting an opportunity to talk to David, as he is an incredibly intelligent and thoughtful person. Better still, he always brings a fresh perspective to topics that I appreciate greatly.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In this case we got to talking about his Biztalk presentation, which he delivered at Tech Ed. Unfortunately I missed the talk due to other commitments, but I did get some of the salient bits from our conversation.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">David put forth that the SOA world is divided into three things: services, objects and data. Services interact with each other following SOA principles of loose coupling and message-based communication. Services are typically composed of objects. Objects interact with data &#8211; typically stored in databases.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">All of this makes sense to me, and meshes well with my view of how services fit into the world at large. Unfortunately we had to cut the conversation short, as I had a Cabana session to deliver with <a href="http://www.neward.net/ted/weblog/index.jsp">Ted Neward</a>, <a href="http://www.vergentsoftware.com/blogs/ckinsman/default.aspx">Chris Kinsman </a>and <a href="http://weblogs.asp.net/kpleas/">Keith Pleas</a>. Interestingly enough, Ted and I got into some great discussions with the attendees of the session about SOA, the role of objects and where (or if) object-relational mapping has any value.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But back to my SOA conversation with David. David&#8217;s terminology scheme is nice, because it avoids the use of the word &#8216;application&#8217;. Trying to apply this word to an SOA world is problematic because it becomes rapidly overloaded. Let&#8217;s explore that a bit based on my observations regarding the use of the word &#8216;application&#8217;.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Applications expose services, thus implying that applications are &#8220;service hosts&#8221;, or that services are a type of interface to an application. This makes sense to most people.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">However, we are now talking about creating SOA applications. These are applications that exist only because they call services and aggregate data and functionality from those services. Such applications may or may not host services in and of themselves.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If that wasn&#8217;t enough, there&#8217;s the idea being that tiers <i style="mso-bidi-font-style: normal">within an application</i> should expose services for use by other tiers in the application. It is often postulated that these tier-level services should be public for use by other applications as well as the &#8216;hosting&#8217; application.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So now things are very complex. An application is a service. An application hosts services. An application is composed of services. An application can contain services that may be exposed to other parts of itself and to others. Oy!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Thus, the idea of avoiding the word &#8216;application&#8217; strikes me as being a Good Thing&#8482;.</font>


> <font face="Times New Roman" color="#000000" size="3"><em>The use of the trademark symbol for this phrase flows, as far as I know, from J. Michael Straczynski (jms). It may be a bit of Babylon 5 insider trivia, but every time I use the phrase, the&nbsp;&#8482; goes through my head...</em></font>


<font face="Times New Roman" color="#000000" size="3">Later in the conference, David and I met up again and talked further. In the meantime I&#8217;d been thinking that something was missing from David&#8217;s model. Specifically, it is the people. Not only users, but other people that might interact with the overall SOA system at large. David put forth that there&#8217;s a couple other things in the mix &#8211; specifically user interfaces and workflow processes, and that this is where the people fit in.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">However, I think there&#8217;s a bit more to it than this. I think that for an SOA model to be complete, the people need to truly fit into the model itself. In other words, they must become active participants in the model in the same way that services, objects and data are active participants. Rather than saying that a user interface is another element of the model, I propose that the <i style="mso-bidi-font-style: normal">human</i> become another element of the model.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">As an aside, I realize that there&#8217;s something a bit odd or even scary about treating human beings as just another part of a system model, but I think there&#8217;s some value in this exercise. This is no different than what business process analysts do when they are looking at manufacturing processes. Humans are put at the same level as machines that are part of the process and are assigned run rates, costs, overhead and so forth. From that perspective, applying this same view to software seems quite valid to me.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So, the question then becomes whether a human is a new entity in the model, or is a sub-type of service, object or data. The way to solve this is to see if a human can fit the role of one of the three pre-existing model concepts.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">My first instinct was to view a human as a service. After all, services interact with other services, and the human interacts with our system and visa versa. However, services interact using loose coupled, message-based communication. Typically our systems interact with users through a Windows or Web interface. This is not message-based, but rather is really quite tightly coupled. We give the user specific, discrete bits of data and we get back specific, discrete bits of data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly there are examples of message-based interaction with humans. For instance, some systems send humans an email or a fax, and the human later responds in some fashion. Even in this case, however, the human&#8217;s response is typically tightly coupled rather than message-based.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Ultimately, then, I don&#8217;t think we can view a human as a type of service due to the violation of SOA communication requirements.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">How about having a human be an object? Other than the obvious puns about objectification of humans (women, men or otherwise), this falls apart pretty quickly. Objects live inside of services and interact with other objects within that service. While it is certainly true that objects use tightly coupled communication, and so do humans, I think it is hard to argue that a human is contained within a given service.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Only one left. Are humans data? Data is used by objects within a service. More generally, data is an external resource that our system uses by calling a service, which uses its objects to interact with this external&nbsp;resource. Typically this is done by calling stored procedures, where we send the resource a set of discrete data or parameters, and the resource returns a set of discrete data.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This sounds terribly similar to how our system interacts with humans. If we turn the idea of a user interface on its head, we could view our system as the actor, and the human as a resource. In such a case, when we display data on a screen, we are basically providing discrete data parameters to a resource (the human) in much the same way we provide parameters to a database via a stored procedure call. The human then responds to our system by providing a set of results in the form of discrete data. This could easily be viewed as equivalent to the results of a stored procedure call.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Following this train of thought, a human really can be viewed as a resource very much like a data source. Any user interfaces we implement are really nothing more than a fancy data access layer within a service. A bit more complex than ADO.NET perhaps, but still the same basic concept. Our system needs to retrieve or alter data and we&#8217;re calling out to an external resource to get it.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I put this idea forward to David, who thought it sounded interesting, but didn&#8217;t see where it helped anything. I can&#8217;t say that I&#8217;m convinced that it helps anything either, but intuitively I think there&#8217;s value here.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I think the value may lie in how we describe our overall system. And this is important, because SOA is all about the overall systems in our organizations. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Nothing makes this more evident than Biztalk 2004 and its orchestration engine. This tool is really all about orchestrating services together into some meaningful process to get work done. However, people are part of almost any real business process, which implies that somewhere in most Biztalk diagrams there should be people. But there aren&#8217;t. Maybe that&#8217;s because people aren&#8217;t services, so Biztalk can&#8217;t interact with them directly. Instead, Biztalk needs to interact with services that in turn interact with the people as a resource &#8211; asking for them to provide data, or to perform some external action and report the result (which is again, just data).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Then again, maybe my thought processes are just totally randomized after being on the road for four weeks straight and this last week being Tech Ed, which is just a wee bit busy (day and night)&#8230; I guess only time will tell. When we start seeing humans show up in our system diagrams we&#8217;ll get a better idea how and where we, as a species, fit into this new SOA world order.</font>
