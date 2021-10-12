---
title: CSLA 4 data portal changes
postDate: 2010-04-03T00:36:03.0070808-05:00
abstract: 
postStatus: publish
---
03 April 2010

This is the first of a series of blog posts I’m putting together as I prepare for the next preview release of CSLA 4. That preview release is coming soon, there are just a couple more things to wrap up, but I want to have the preview out by the .NET 4 launch, which is April 12.

CSLA 4 includes a lot of changes, including some changes to the data portal. This post covers the highlights.

## DataPortal methods

Some are relatively small, but might impact existing code.

One example is the removal of the non-generic DataPortal method overloads. Create() is gone in favor of Create&lt;T&gt;().

Another example is that DataPortal\_Fetch(object) is no longer a virtual method in the base classes, which means if you are overriding this method you’ll need to remove the override keyword in your code.

The reason for removing the non-generic DataPortal methods is that it makes the criteria parameter for Create/Fetch/Delete more flexible. It is now possible to use any serializable object as a criteria. On .NET this means anything that can be serialized with the BinaryFormatter and/or NDCS. On Silverlight this means anything that can be serialized with MobileFormatter. And this includes primitive types. In short, you can now do this:


> var cust = DataPortal.Fetch&lt;Customer&gt;(123);


This eliminates the need for the SingleCriteria&lt;&gt; type, and generally simplifies most data portal calls.

## Proxy factory

A more significant change, though one that has no impact unless you want to use it, is the ability to create your own proxy factory. By default the data portal loads the client-side proxy based on the type you specify in your config file – so you can switch between local, WCF, Remoting and other proxies through configuration.

But it is now possible to create a proxy factory by implementing IDataPortalProxyFactory. This factory is responsible for creating the data portal proxy object based on the type of business object being sent through the data portal. Add a key in your config file for CslaDataPortalProxyFactory to specify the assembly qualified type of your implementation and CSLA will use that instead of the default behavior.

The idea is that some applications need to use different app servers or different protocols for different business objects. If you create your own proxy factory, you get the opportunity to examine the business object type (probably using reflection) so you can decide which proxy should be used to talk to an app server for that particular type of object.

## Server exceptions

(not implemented yet, but in progress)

Server exceptions are always returned to the client wrapped in a DataPortalException. This is not changing, because the DataPortalException is what allows CSLA to provide you with the full stack trace and other useful information from the server.

However, it is now possible to replace the original server exception with a new exception in your override of DataPortal\_OnDataPortalException() or the InvokeError() method of a factory object.

## Silverlight flexibility

The Silverlight data portal was not as flexible as the .NET data portal. Specifically, it wasn’t possible to create your own proxy/host channel that totally replaced the WCF proxy/host provided by CSLA. In CSLA 4 you can now create completely custom proxy/host channels for the Silverlight data portal. This means you could, for example, create one that didn’t use WCF at all, but instead used raw TCP sockets. Or more likely, it means you can create a proxy/host that uses a custom third-party WCF binding.

A related change is to the MobileFormatter, which now has the ability to provide you with completely serialized data (the default), or to provide you with the serialized data in an intermediate DTO form. If you get the DTO form, you are getting an object graph that consists only of objects which can be serialized using the DataContractSerializer (or similar serializers). This opens up a lot of flexibility, because it means you can apply other serializers (perhaps from third parties) to the DTO graph. In some cases this

## Design time data

VS10 has a new design time data model, so the old design time data behaviors have been removed from the data portal. This won’t break any code, but if you were using the design time data generation concept, it is now gone and your methods won’t be invoked.

## .NET compression sample

There’s a new sample for .NET that shows how to use a standard compression library (of your choice) to compress the data that goes over the data portal. I think it is probably best to get a WCF binding that does the compression, but if you want an alternative this sample shows you how to do it.

Overall the data portal continues to offer the same n-tier and network transport flexibility it has always provided, but these changes make common scenarios easier to implement, and enable some important advanced scenarios that have been frequently requested.
