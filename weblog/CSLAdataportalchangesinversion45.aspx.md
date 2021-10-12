---
title: CSLA data portal changes in version 4.5
postDate: 2012-07-30T23:53:23.6852031-05:00
abstract: 
postStatus: publish
---
30 July 2012

I want to summarize some of the more major changes coming to the data portal in CSLA 4 version 4.5. Some of these are breaking changes.

I’ve done four big things with the data portal:

1. Added support for the new async/await keywords on the client and server
2. Merged the .NET and Silverlight data portal implementations into a single code base that is now common across WinRT, .NET, and Silverlight
3. Removed the public virtual DataPortal\_XYZ method definitions from Silverlight, because it can now invoke non-public methods just like in .NET. Also, all local Silverlight data portal methods no longer accept the async callback handler, because they now support the async/await pattern
4. Remove the ProxyMode concept from the Silverlight data portal, because the RunLocal attribute is now available on all platforms


All four have some level of breaking change.

Adding comprehensive support for async/await changes the way .NET handles exceptions. Although I’ve worked to keep the *top level* exceptions consistent, the actual exception object graph (nested InnerExceptions) will almost certainly be different now.

Merging the .NET and Silverlight data portal implementations introduces a number of relatively minor breaking changes for Silverlight users. Though if you’ve created custom proxy/host pairs or other more advanced scenarios you might be more affected than others. There may also be unintended side-effects to .NET users. Some might be bugs, others might be necessary to achieve platform unification.

Removing the public virtual DataPortal\_XYZ methods from BusinessBase and BusinessListBase will break anyone using the local Silverlight data portal. The fix is minor – just change the public scopes to protected. This change shouldn’t affect anyone using .NET, or using a remote data portal from Silverlight.

Removing the async callback parameter from all Silverlight client-side DataPortal\_XYZ methods will break anyone using the local Silverlight data portal. The fix is to switch to the new async/await pattern. The code changes are relatively minor, and generally simplify your code, but if you’ve made extensive use of the client-side data portal in Silverlight this will be a pretty big change I’m afraid.

Similarly, removing the ProxyMode concept from the Silverlight data portal is a breaking change for people using the local Silverlight data portal. Again, the fix is pretty simple – just add the RunLocal attribute to the DataPortal\_XYZ (or object factory) methods as you have always done in .NET.

On the upside, the coding patterns for writing code in .NET, WinRT, and Silverlight are now the same.

For example, a DataPortal\_Fetch method *on any platform* looks like this:


> private void DataPortal\_Fetch(int id)


or like this


> private async Task DataPortal\_Fetch(int id)


The data portal will automatically detect if your method returns a Task and it will await the method, allowing you to use the await keyword inside your DataPortal\_XYZ methods.

Similarly, all platforms can now write this client-side code:


> var obj = await CustomerEdit.GetCustomerAsync(123);


or the older event-style code:


> CustomerEdit.GetCustomer(123, (o, e) =&gt;
>   {
>       if (e.Error != null)
>           throw e.Error;
>      else
>           obj = e.Object;
>   });


Only .NET code can use the synchronous approach:


> var obj = CustomerEdit.GetCustomer(123);


This is one of the few platform-specific concepts left in the data portal.

What is really cool is that the client and server sync/async concepts can be mixed (as long as you know what to expect).


| Client method | Client platform | Server method | Server platform | Remarks |
| --- | --- | --- | --- | --- |
| Fetch | .NET only | void DataPortal\_Fetch | any | Client call is synchronous; server call is synchronous |
| Fetch | .NET only | Task DataPortal\_Fetch | any | Client call is synchronous; server call is asynchronous; note that client will block until the server’s work is complete |
| BeginFetch | any | void DataPortal\_Fetch | any | Client call is asynchronous (event-based); server call is synchronous; client will not block, and must handle the callback event to be notified when the server call is complete |
| BeginFetch | any | Task DataPortal\_Fetch | any | Client call is asynchronous (event-based); server call is asynchronous; client will not block, and must handle the callback event to be notified when the server call is complete |
| FetchAsync | any | void DataPortal\_Fetch | any | Client call is asynchronous; server call is synchronous; client will block or not, depending on how you invoke the client-side Task (using await or other techniques); the client-side Task will complete when the server call is complete |
| FetchAsync | any | Task DataPortal\_Fetch | any | Client call is asynchronous; server call is asynchronous; client will block or not, depending on how you invoke the client-side Task (using await or other techniques); the client-side Task will complete when the server call is complete |


I expect all client-side data portal code to switch to the async/await versions of the methods, and so I’ve made them the mainline path through the data portal. The synchronous and event-based async methods use async/await techniques behind the scenes to do implement the desired behaviors.

There is a lot of variety in how you can invoke an awaitable method like FetchAsync. The specific async behaviors you should expect will vary depending on how you invoke the method. For example, there’s a big difference between using the await keyword or the Result or RunSynchronously methods:


> var obj = await CustomerEdit.GetCustomerAsync(123);
>
> var obj = CustomerEdit.GetCustomerAsync(123).Result;


The former is async, the latter is sync. The former will return a simple exception (if one occurs), the latter will return an AggregateException containing the simple exception. This has little to do with CSLA, and nearly everything to do with the way the async/await and task parallel library (TPL) are implemented by .NET.

Finally, I do need to state that the actual network transport (typically WCF) used by .NET, Silverlight, and WinRT aren’t the same. This is because WCF in .NET is far more flexible than in Silverlight or WinRT. And because the WCF client-side proxies generated for Silverlight use event-driven async methods, and in WinRT the proxy is task-based.

The data portal hides these differences pretty effectively, but you should understand that they exist, and as a result there may be subtle behavioral differences between platforms, especially when it comes to exceptions and exception details. The success paths for creating, fetching, updating, and deleting objects are identical, but there may be edge cases where differences exist.

All in all I am quite pleased with how this is turning out. I’ve put a massive amount of work into the data portal for 4.5, especially around unifying the implementations across platforms. I suspect there’ll be some issues to work through during the beta testing phase, but the end result is a far more consistent, maintainable, and streamlined codebase for all platforms. That will benefit all of us over time.
