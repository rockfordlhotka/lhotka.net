---
title: DNR TV show on CSLA .NET and data access
postDate: 2007-04-19T09:44:40.4631888-05:00
abstract: 
postStatus: publish
---
19 April 2007

I was [out of touch](http://www.lhotka.net/weblog/HealthWoes.aspx) for a while there, and so I couldn't post about this.

But there's a recent .NET Rocks TV (DNR TV) show where I discuss various data access options for use with CSLA .NET. These include:

1. Using the approach from my books: the datareader directly in the object
2. Separating the database connection/command code into a different assembly
3. Separating the whole data access into a different assembly and using data transfer objects (DTOs) to transfer the data into the business objects
4. Calling a web service to get the DTOs into the objects (so putting the data access not only in a different assembly, but putting them behind a web service)


[Click here](http://www.dnrtv.com/default.aspx?showID=60) to get to the DNR TV show page. I also showed [this demo](http://www.lhotka.net/Article.aspx?area=11&amp;id=65c98c98-f0e0-477d-b45b-7a1e7d5768ee) at [VS Live](http://www.vslive.com) in San Franscisco, and will show it again in Orlando in May.

Subsequent to that DNR TV show, I've enhanced the demo to also use LINQ to create the DTOs, and to use VB's late binding capability to make it possible to load the business object with data from the local DTO, the web service DTO and the LINQ DTO without any change to code (remember that web service proxies and LINQ create their own DTO types - so even though they are the same *shape*, they are actually different types - this is *exactly* where dynamic language features come in very handy!)

I haven't put the LINQ code online yet, but I will within the next few weeks as I catch up on everything.
