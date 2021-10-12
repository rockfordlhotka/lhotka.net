---
title: CSLA .NET and Windows Azure
postDate: 2011-03-27T19:11:17.1106835-05:00
abstract: 
postStatus: publish
---
27 March 2011

I have been working on the *Using CSLA 4: Data Portal Configuration* ebook, part of the [Using CSLA 4 ebook series](http://store.lhotka.net/Default.aspx?tabid=1560&amp;ProductID=22). One section of the book covers the use of Windows Azure as the application server, where the server-side components of the CSLA .NET data portal and your application will run.

Perhaps the most interesting part of that section of the ebook is that there’s no meaningful difference between hosting in Windows Azure and hosting in IIS on an on-premise Windows Server. In fact, the only difference at all is that the project in Visual Studio is an Azure ASP.NET Web Role project instead of an Empty ASP.NET web project.

This is because Windows Azure allows WCF services to host in a web role in the same way IIS hosts WCF services. When using the WCF data portal channel, the server components are accessed through a standard WCF endpoint – nothing special or fancy. That means any place you can host WCF, you can host the data portal.

In my example solution, there’s also a Silverlight client app. It is part of that same Web Role app, so a user simply navigates to the web page in Azure that hosts the Silverlight app. The Silverlight app runs on the client, and uses the data portal to interact with the server-side components of the application running in Azure.

There is some potential value to hosting the data portal (your application server) in Windows Azure.

There’s the obvious scalability benefit. Because the data portal is stateless, and typical server-side business code in a CSLA application is also stateless, there is no problem with just adding more web role instances to the app. If more capacity is required on the server, just change the Azure configuration and just like that you have more capacity.

The business code running in Azure typically implements persistence. Another value of running the application server in Azure is that the application can store its data in SQL Azure. Pretty comparable to SQL Server, but based in the cloud. In that way, the entire app can be cloud-based, with the Silverlight client using client-side CPU and memory resources, while the rest of the app scales happily in Azure.

Alternately, the application could store its data in Azure Storage. That isn’t a relational data store, but does offer some interesting super-scaling capabilities that may be quite valuable.

In the end, perhaps the most notable thing to consider is this: when building an application using CSLA and the data portal, it is entirely possible to switch between hosting in IIS to hosting in Azure, and back again, without changing anything except the application configuration.

Sure, if you use Azure-specific features in your business code (like Azure Storage), you can’t easily move off Azure. But if you stick with SQL Server or SQL Azure, and avoid Azure Storage, the .NET Service Bus, and other Azure-specific constructs, CSLA can help you build an app that can exploit Azure, without being locked into Azure forever.
