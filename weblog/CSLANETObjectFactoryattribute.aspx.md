---
title: CSLA .NET ObjectFactory attribute
postDate: 2008-08-15T15:16:41.265-05:00
abstract: 
postStatus: publish
---
15 August 2008

One of the features we added in CSLA Light was the idea of a "factory" or "observer" object - kind of like a police sobriety checkpoint - that can be called when any data portal request comes in from the client. This is a server-side object that can examine or manipulate the business object or criteria object sent from the client, before any other server-side processing is allowed.

I liked the idea so much that I decided to put it into the CSLA .NET 3.6 data portal too. Which turned out to be *much* harder than I expected...

Of course I don't want to break compatibility with the current data portal behavior, so it must continue unchanged.

But if you put the ObjectFactory attribute on your business class, that should redirect the data portal to create an instance of the factory object you specify, and to route all data portal calls to methods on *that* object instead of calling DataPortal\_XYZ as normal.

For example:


> [ObjectFactory("Factories.MyFactory,Factories")]
> [Serializable]
> public class CustomerEdit : BusinessBase&lt;CustomerEdit&gt;


This tells the data portal to *not* call any DataPortal\_XYZ methods, but instead to create an instance of a MyFactory object and to call methods named Create(), Fetch(), Update() and Delete() on that object instead.

This is extensible in numerous ways. You can specify the names of the four methods. You can provide a "factory loader" so that string parameter passed to ObjectFactory can be interpreted differently - how ever you'd like. The *default* factory loader treats that string like an assembly qualified type name, because I think that's what most people will want.

So you have to create MyFactory:


> namespace Factories
> {
>   public class MyFactory
>   {
>     [RunLocal]
>     public object Create()
>     {
>       // create object here
>       return obj;
>     }
>
>     public object Fetch(SingleCriteria&lt;CustomerEdit, int&gt; criteria)
>     {
>       // retrieve object here
>       return obj;
>     }
>
>     [Transactional(TransactionTypes.TransactionScope)]
>     public object Update(CustomerEdit obj)
>     {
>       // insert/update/delete object here
>     }
>
>     [Transactional(TransactionTypes.TransactionScope)]
>     public void Delete(SingleCriteria&lt;CustomerEdit, int&gt; criteria)
>     {
>       // delete data here
>     }
>   }
> }


Normal method overloading rules apply to these methods. So you can have multiple Fetch() methods with different criteria object types and the data portal will call the right method. This is exactly the same behavior as with DataPortal\_Create(), DataPortal\_Fetch() and DataPortal\_Delete() today.

Notice that the RunLocal and Transactional attributes can be applied to these methods just like they would have been applied to the DataPortal\_XYZ methods.

RunLocal is interesting though, because it obviously can only work if you deploy your factory assembly to the client along with the business assembly. In most cases I expect people won't choose to do that, and so won't be able to use RunLocal.

The default for Transactional is to use Manual transactions. In other words, if you don't use the attribute it is entirely up to your factory method to handle any transaction details.

It is *very important* to realize that when using this factory model, the data portal does virtually nothing for you. It doesn't automatically call MarkOld(), MarkNew() or MarkAsChild(). You assume *total responsibility* for creating and initializing the business object graph, and for setting the state of all objects in the graph.
