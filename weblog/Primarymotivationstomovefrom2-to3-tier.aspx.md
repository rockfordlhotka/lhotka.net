---
title: Primary motivations to move from 2- to 3-tier
postDate: 2007-11-13T16:37:50.65788-06:00
abstract: 
postStatus: publish
---
13 November 2007

I always encourage people to go with 2-tier deployments if possible, because more tiers increases complexity and cost.

But it is important to recognize when the value of 3-tier outweighs that complexity/cost. The primary three motivators are:

1. **Security** – using an app server allows you to shift the database credentials from clients to the server, adding security because a would-be hacker (or savvy end-user) would need to hack into the app server to get those credentials.
2. **Network infrastructure limitations** – sometimes a 3-tier solution can help offload processing from CPU-bound or memory-bound machines, or it can help minimize network traffic over slow or congested links. Direct database communication is a chatty dialog, and using an app server allows a single blob of data to go across the slow link, and the chatty dialog to occur across a fast link, so 3-tier can result in a net win for performance if the client-to-server link is slow or congested.
3. **Scalability** – using an app server provides for database connection pooling. The trick here, is that if you don’t need it, you’ll *harm performance* by having an app server, so this is only useful if database connections are taxing your database server. Given the state of modern database hardware/software, scalability isn’t a big deal for the vast majority of applications anymore.


The [CSLA .NET](http://www.lhotka.net/cslanet) data portal is of great value here, because it allows you to switch from 2-tier to 3-tier with a configuration change - no code changes required\*. You can deploy in the cheaper and simpler 2-tier model to start with, and if one of these motivators later justifies the complexity of moving to 3-tier, you can make that move with relative ease.

\* disclaimer: if you plan to make such a move, I *strongly* suggest testing in 3-tier mode during development. While the data portal makes this 2-tier to 3-tier switch seamless, it only works if the code in the business objects follows all the rules around serialization and layer seperation. Testing in a 3-tier mode helps ensure that none of those rules get accidentally broken during development.
