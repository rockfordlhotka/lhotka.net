---
title: More data portal enhancements for CSLA 4.5
postDate: 2012-10-01T15:26:41.7960555-05:00
abstract: 
postStatus: publish
---
01 October 2012

I just checked in a series of data portal enhancements that have been on the wish list for a while. Mostly focused on pre- and post-processing behaviors.

The big one is that you can now provide an IInterceptDataPortal provider on the server to get Initialize and Complete notifications for every data portal call, allowing for logging/tracing and IoC scenarios. The logging/tracing is probably obvious, because these methods get a lot of detail about each data portal server invocation and you can do what you’d like with that data. The IoC scenario may be less obvious, but the Initialize method should provide you with a consistent way to create or retrieve your server-side IoC container so it is available for the duration of the server-side processing. I suspect most people will put the container instance in Csla.Application.LocalContext to ensure it is easily and consistently available to all code regardless of runtime environment (ASP.NET, pure .NET, WinRT, Silverlight).

The existing pre- and post-processing calls now all get a lot more data than they did before, so they should be more useful by far. The primary focus was on the Invoke, InvokeComplete, and InvokeException methods in factory objects, where the previous implementation was poor. In that context I did make <font style="background-color: #ffff00">a breaking change</font>, because those methods are now passed a Csla.DataPortalEventArgs value as a parameter, instead of the more limited DataPortalContext they got before.

While I was doing this change though, I also increased the amount of data provided to the pre and post-processing DataPortal\_XYZ and Child\_XYZ style methods. So everyone gets an upgrade ![Smile](binary/Windows-Live-Writer/More-data-portal-enhancements-for-CSLA.5_D78F/wlEmoticon-smile_2.png)

Finally, the data portal no longer returns the business object to the client when an exception happens – at least by default. Up to this point the data portal has always returned the business object from the server to the client via the DataPortalException, but almost no one actually uses that value. By not returning it, we save a bunch of network traffic and improve performance. If you *want* the value, you can configure the data portal to use the older behavior. So this is <font style="background-color: #ffff00">a breaking change</font>, but one with an easy workaround.
