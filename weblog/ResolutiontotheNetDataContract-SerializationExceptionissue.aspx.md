---
title: Resolution to the NetDataContract/SerializationException issue
postDate: 2007-06-11T10:07:53.767-05:00
abstract: 
postStatus: publish
---
11 June 2007

I [posted previously](http://www.lhotka.net/weblog/WCFNetDataContractSerializerAndSecurityException.aspx)about an issue where the WCF NetDataContractSerializer was unable to serialize a SecurityException object. Microsoft provided some insight.

It turns out that the constructor of the SerializationException object doesn't set the Action property to anything valid. Before you can serialize a SerializationException with NDCS you must explicitly set the Action property to a valid SecurityAction.

This *does mean* that NDCS is not compatible with the BinaryFormatter in this case, but at least there's a workaround/solution.

I've now updated CSLA .NET 3.0 to explicitly set the Action property any time a SecurityException is thrown, thus allowing the WCF data portal channel to return valid details about the nature of any exception.
