---
title: Calling Roles.GetRolesForUser in a WCF service
postDate: 2011-04-28T18:46:57.4792121-05:00
abstract: 
postStatus: publish
---
28 April 2011

Today I spent hours trying to make one line of code work. Fortunately [Miguel Castro](http://dotnetdude.com/) was ultimately able to help me troubleshoot the issue thanks to his deep understanding of all things ASP.NET.

The line of code seems so simple:


> var data = Roles.GetRolesForUser(“rocky”);


In this case *Roles* is the RoleProvider API from System.Web.Security, and the method returns a string array with the roles for the user.

This line of code works great in my aspx page. No problem at all.

But *in the same web project* it throws a NullReferenceException when called from a WCF service (in a svc).

No stack trace. No detail. No nothing. I Binged, and Googled, and created a whole new solution (figuring my first solution was somehow corrupted). But nothing helped.

To cut to the answer, this works in a WCF service:


> var data = Roles.Provider.GetRolesForUser(“rocky”);


See the difference? Instead of relying on the static helper method on the Roles type, this code explicitly calls the method on the default provider instance.

(fwiw, I think this behavior is relatively new, because that code *used to work*. I just don’t remember how long ago it was that it worked – .NET 3 or 3.5 – so perhaps something broke in .NET 4?)

In any case, problem solved – thanks Miguel!!
