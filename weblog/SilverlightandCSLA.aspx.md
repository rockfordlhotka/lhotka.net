---
title: Silverlight and CSLA
postDate: 2007-05-01T17:25:03.9464288-05:00
abstract: 
postStatus: publish
---
01 May 2007

This week Microsoft fully disclosed their plans for [Silverlight](http://www.microsoft.com/silverlight). It is not only a way to build rich internet applications (RIAs), but it is a way to build them with .NET! This is very exciting news, and I hope that Microsoft follows through on their vision for Silverlight!!

With the support of [Magenic](http://www.magenic.com), I've been researching the possibility of creating a CSLA Light which *would* run in an Internet zone sandbox, and in the even more restrictive Silverlight environment. The Silverlight 1.1 alpha available today doesn't have enough functionality to even come close to hosting something like CSLA, but Microsoft's plan for Silverlight should provide enough functionality to create a stripped down, client only version of CSLA.

That means no data portal, no Clone() method, and the requirement to implement GetState() and SetState() methods to support n-level undo (thanks to no private reflection). But it does mean that I should be able to provide the full validation, authorization, data binding and n-level undo capabilities of CSLA .NET in the CSLA Light version.

I also plan to provide the data portal *interface* so factory methods can remain consistent, but the back-end implementation will be quite different. (I can't do mobile objects due to no serialization, and I can't do the strongly-typed DP\_XYZ calls due to no private reflection). The lack of a real data portal is pretty hard to take, but I haven't figured out a way to do it, so it is probably unavoidable...

I anticipate that around 80% of the code you'd write in a business object today will be the same in CSLA Light, perhaps even more.

Thanks to the compatibility between Silverlight and WPF/.NET itself, there are some other interesting possiblities for CSLA Light. Code written for Silverlight should always run in a less restrictive environment like WPF on Windows, or even XBAP/WPF in a browser. Due to this, CSLA Light will almost certainly work in those settings as well.

In any case, this will be a somewhat slow moving initiative, because I have to wait until Microsoft comes out with a release of Silverlight that supports key WPF features like data binding before I can get too far with the project...
