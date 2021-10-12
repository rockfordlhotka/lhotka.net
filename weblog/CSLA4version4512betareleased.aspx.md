---
title: CSLA 4 version 4.5.12 beta released
postDate: 2013-02-20T17:30:19.8037119-06:00
abstract: 
postStatus: publish
---
20 February 2013

First: CSLA .NET has moved to GitHub and has a new home page: http://www.cslanet.com

Second, the most recent beta version 4.5.12, is now available for download and through nuget. There are a couple bug fixes, and some server-side data portal enhancements to better support the use of IoC containers for creating business objects when using the encapsulated data portal model.

In summary, you can create an implementation of Csla.Server.IDataPortalInterceptor where you can implement code that runs at the very start and very end of *every single data portal call*. Then you can create an implementation of Csla.Server.IDataPortalActivator where you can assume responsibility for creating an instance of the requested business type, and for initializing the object instance (thus supporting property injection).

Along with this, the data portal now allows you to use interfaces instead of concrete types (assuming you've supplied an IDataPortalActivator of course):


> var obj = Csla.DataPortal.FetchAsync&lt;IPersonEdit&gt;();


In this example, the 'obj' reference might be any type that implements IPersonEdit, and the actual concrete type is determined by your IDataPortalActivator implementation. The default implementation is to create an instance of the supplied type, so the supplied type must be a concrete type. As a result, no existing code is affected by this change.
