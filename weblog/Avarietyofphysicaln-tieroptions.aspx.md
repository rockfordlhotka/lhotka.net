---
title: A variety of physical n-tier options
postDate: 2005-07-23T12:12:25.21875-05:00
abstract: There are three broad models for 3-tier deployment of your application's layers - here's an overview
postStatus: publish
---
23 July 2005

<font face="Times New Roman" color="#000000" size="3">In my </font>[<font face="Times New Roman" size="3">last post</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=efa88d0a-2388-4909-bee1-c9bddb6e9868)<font face="Times New Roman" color="#000000" size="3"> I talked about logical layers as compared to physical tiers. It may be the case that that post (and this one) are too obvious or basic. But I gotta say that I consistently am asked about these topics at conferences, user groups and via email. The reality is that none of this is all that obvious or clear to the vast majority of people in our industry. Even for those that truly </font>[<font face="Times New Roman" size="3">grok</font>](http://en.wikipedia.org/wiki/Grok)<font face="Times New Roman" color="#000000" size="3"> the ideas, there’s far from universal agreement on how an application should be layered or how those layers should be deployed onto tiers.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In one comment on my previous post Magnus points out that my portrayal of the application server merely as a place for the Data Access layer flies in the face of Magnus’ understanding of n-tier models. Rather, Magnus (and many other people) is used to putting both the Business and Data Access layers on the application server, with only the Presentation layer on the client workstation (or presumably the web server in the case of a web application, though the comment didn’t make that clear).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The reality is that there are three primary models to consider in the smart/rich/intelligent client space. There are loose analogies in the web world as well, but personally I don’t find that nearly as interesting, so I’m going to focus on the intelligent client scenarios here.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Also one quick reminder – tiers should be avoided. This whole post assumes you’ve justified using a 3-tier model to obtain scalability or security as per my previous post. If you don’t need 3-tiers, don’t use them – and then you can safely ignore this whole entry :)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">There’s the <i style="mso-bidi-font-style: normal">thick client</i> model, where the Presentation and Business layers are on the client, and the Data Access is on the application server. Then there’s the <i style="mso-bidi-font-style: normal">thin client</i> model where only the Presentation layer is on the client, with the Business and Data Access layers on the application server. Finally there’s the <i style="mso-bidi-font-style: normal">mobile object</i> model, where the Presentation and Business layers are on the client, and the Business and Data Access layers are on the application server. (Yes, the Business layer is in two places) This last model is the one I discuss in my </font>[<font face="Times New Roman" size="3">Expert VB.NET and C# Business Objects</font>](http://www.lhotka.net/cslanet)<font face="Times New Roman" color="#000000" size="3"> books and which is supported by my CSLA .NET framework.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The benefit to the thick client model is that we are able to provide the user with a highly interactive and responsive user experience, and we are able to fully exploit the resources of the client workstation (specifically memory and CPU). At the same time, having the Data Access layer on the application server gives us database connection pooling. This is a very high scaling solution, with a comparatively low cost, because we are able to exploit the strengths of the client, application and database servers very effectively. Moreover, the user experience is very good and development costs are relatively low (because we can use the highly productive Windows Forms technology).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The drawback to the thick client model is a loss of flexibility – specifically when it comes to process-oriented tasks. Most applications have large segments of OLTP (online transaction processing) functionality where a highly responsive and interactive user experience is of great value. However, most applications also have some important segments of process-oriented tasks that don’t require any user interaction. In most cases these tasks are best performed on the application server, or perhaps even directly in the database server itself. This is because process-oriented tasks tend to be very data intensive and non-interactive, so the closer we can do them to the database the better. In a thick client model there’s no natural home for process-oriented code near the database – the Business layer is way out on the client after all…</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Another perceived drawback to the thick client is deployment. I dismiss this however, given .NET’s no-touch deployment options today, and ClickOnce coming in 2005. Additionally, <i style="mso-bidi-font-style: normal">any</i> intelligent client application requires deployment of our code – the Presentation layer at least. Once you solve deployment of one layer you can deploy other layers as easily, so this whole deployment thing is a non-issue in my mind.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In short, the thick client model is really nice for interactive applications, but quite poor for process-oriented applications.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The benefit to the thin client model is that we have greater control over the environment into which the Business and Data Access layers are deployed. We can deploy them onto large servers, multiple servers, across disparate geographic locations, etc. Another benefit to this model is that it has a natural home for process-oriented code, since the Business layer is already on the application server and thus is close to the database.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Unfortunately history has shown that the thin client model is severely disadvantaged compared to the other two models. The first disadvantage is scalability in relationship to cost.<span style="mso-spacerun: yes">&nbsp; </span>With either of the other two models as you add more users you intrinsically add more memory and CPU to your overall system, because you are leveraging the power of the client workstation. With a thin client model all the processing is on the servers, and so client workstations add virtually no value at all – their memory and CPU is wasted. Any scalability comes from adding larger or more numerous server hardware rather than by adding cheaper (and already present) client workstations.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The other key drawback to the thin client model is the user experience. Unless you are willing to make “chatty” calls from the thin Presentation layer to the Business layer across the network on a continual basis (which is obviously absurd), the user experience will not be interactive or responsive. By definition the Business layer is on a remote server, so the user’s input can’t be validated or processed without first sending it across the network. The end result is roughly equivalent to the mainframe user experiences users had with 3270 terminals, or the experience they get on the web in many cases. Really not what we should expect from an “intelligent” client…</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course deployment remains a potential concern in this model, because the Presentation layer must still be deployed to the client. Again, I dismiss this as a main issue any longer due to no-touch deployment and ClickOnce.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In summary, the thin client model is really nice for process-oriented (non-interactive) applications, but is quite inferior for interactive applications.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This brings us to the mobile object model. You’ll note that neither the thick client nor thin client model is optimal, because almost all applications have some interactive and some non-interactive (process-oriented) functionality. Neither of the two “purist” models really addresses both requirements effectively. This is why I am such a fan of the mobile object (or mobile agent, or distributed OO) model, as it provides a compromise solution. I find this idea so compelling that it is the basis for my books.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The mobile object model literally has us deploy the Business layer to both the client and application server. Given no-touch deployment and/or ClickOnce this is quite practical to achieve in.NET (and in Java interestingly enough). Coupled with .NET’s ability to pass objects across the network by value (another ability shared with Java), all the heavy lifting to make this concept work is actually handled by .NET itself, leaving us to merely enjoy the benefits.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The end result is that the client has the Presentation and Business layers, meaning we get all the benefits of the thick client model. The user experience is responsive and highly interactive. Also we are able to exploit the power of the client workstation, offering optimal scalability at a low cost point.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But where this gets really exciting is the flexibility offered. Since the Business layer <i style="mso-bidi-font-style: normal">also</i> runs on the application server, we have all the benefits of the thin client model. Any process-oriented tasks can be performed by objects running on the application server, meaning that all the power of the thin client model is at our disposal as well.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The drawback to the mobile object approach is complexity. Unless you have a framework to handle the details of moving an object to the client and application server as needed this model can be hard to implement. However, given a framework that supports the concept the mobile object approach is no more complex than either the thick or thin client models.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In summary, the mobile object model is great for both interactive and non-interactive applications. I consider it a “best of both worlds” model and CSLA .NET is specifically designed to make this model comparatively easy to implement in a business application.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">At the risk of being a bit esoteric, consider the broader possibilities of a mobile object environment. Really a client application or an application server (Enterprise Services or IIS) are merely hosts for our objects. Hosts provide resources that our objects can use. The client “host” provides access to the <i style="mso-bidi-font-style: normal">user resource</i>, while a typical application server “host” provides access to the <i style="mso-bidi-font-style: normal">database resource</i>. In some applications you can easily envision other hosts such as a batch processing server that provides access to a <i style="mso-bidi-font-style: normal">high powered CPU resource</i> or a <i style="mso-bidi-font-style: normal">large memory resource</i>.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Given a true mobile object environment, objects would be free to move to a host that offers the resources an object requires at any point in time. This is very akin to grid computing. In the mobile object world objects maintain both data and behavior and merely move to physical locations in order to access resources. Raw data never moves across the network (except between the Data Access and Data Storage layers), because data without context (behavior) is meaningless.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course some very large systems have been built following both the thick client and thin client models. It would be foolish to say that either is fatally flawed. But it is my opinion that neither is optimal, and that a mobile object approach is the way to go.</font>
