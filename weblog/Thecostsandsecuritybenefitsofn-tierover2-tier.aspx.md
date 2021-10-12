---
title: The costs and security benefits of n-tier over 2-tier
postDate: 2007-12-21T10:55:19.1258512-06:00
abstract: 
postStatus: publish
---
21 December 2007

I recently received this email:


> *Thank you very much for your insightful articles concerning 2 vs. 3 tier models.  It’s very refreshing to hear a view point that I’m aligned with.  Here at work I’m dealing with network Nazi’s who believe there is no cost of a middle tier and that there is only huge security rewards to reap.  I use your articles to support my point but I’m still not getting tremendously far.  I have yet to have anyone explain to me exactly how that middle tier is going to really add a significant enough amount of security that will warrant the high price to pay for employing a performance blasting middle-man.*


There are two scenarios, though they are similar.

In the web, adding a middle tier has a very high cost, because the web server is *already* an app server. It already does database connection pooling across all users on that server. Adding an app server just adds overhead.

The only exception here is where the web server is serving up a lot of *static content* and only some dynamic content. In that case, moving the data access to another machine may be beneficial because it can allow the web server to focus more on delivering the static content. It is important to realize that the dynamic content will *still be delivered more slowly* due to overhead, but the overall web site may work better.

In Windows, adding a middle tier has a cost because the data needs to make two network hops to get to the user. Each network hop has a tangible cost. It would be foolish to ignore the cost of moving data over the wire, and the cost of serializing/deserializing the data on each end of the wire. These are very real, measurable costs.

In *both*cases the middle tier means an extra machine to license, administer, maintain, power and cool. It is an extra point of failure, extra potential for network/CPU/memory/IO contention, etc. These costs come with every server you add into the mix. Anyone who’s ever been a manager or higher in an IT organization has a very good understanding of these costs, because they impact the budget at the end of every year.

However, the security benefits of a middle tier are real.

In a 2-tier web model the database credentials are on the web server. Even if they are encrypted they are there on that machine. A would-be hacker could get them by cracking into that one machine.

Switching to a 3-tier model moves the database credentials onto the middle tier and off the web server. Now the web server has credentials to the app server, but not the database. A would-be hacker must crack first the web server, then the app server to get those credentials.

In a 2-tier Windows model the database credentials are on each client workstation. Even if they are encrypted they are there on those machines. A would-be hacker could get them by sitting at that machine - all it takes is a little social engineering and they're in. More likely, an *employee* may get the credentials and use Excel or some other common tool to directly access the database, bypassing your application. Oh the havoc they could wreak!

Switching to a 3-tier model moves the database credentials onto the middle tier and off the client workstations. Now the workstations have credentials to the app server, but not the database. A would-be hacker must crack into the app server to get those credentials. And end users are almost automatically shut out, because they would have to be a hacker to get to the app server to get the database credentials.
