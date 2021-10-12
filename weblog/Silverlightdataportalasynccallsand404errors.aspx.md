---
title: Silverlight data portal, async calls and 404 errors
postDate: 2008-10-02T19:16:01.346472-05:00
abstract: 
postStatus: publish
---
02 October 2008

The next release of CSLA .NET for Silverlight will return to using the async WcfProxy in the data portal instead of the SynchronizedWcfProxy that restricts the data portal to allow only one concurrent call at a time. The WcfProxy allows parallel calls from the client to the server through the data portal. The change is already in svn for those that are using live code.

The reason we created SynchronizedWcfProxy originally was due to a bug in Silverlight 2.0 Beta 2, where in some cases you'd get a 404 error with overlapping WCF calls to the same server. This was wreaking havoc with our unit tests, which have a lot of parallel WCF calls.

It appears that the issue is resolved in Silverlight RC0, which is great news.

However, we didn't know right away, because we were still getting sporadic 404 errors. With some research, and help from Eugene Osovetsky and his colleagues at Microsoft, we figured out the remaining issue.

Part of the problem is described by Eugene's [post on dealing with faults and exceptions in Silverlight](http://eugeneos.blogspot.com/2008/09/faults-and-exceptions-when-using-web.html). This was masking the underlying issue we faced.

The underlying issue is that we were testing using the ASP.NET Development Web server (often called Cassini). Cassini has some well-known limitations, among them that it doesn't work well when a custom .NET principal is used in your web server code. This particular issue appears as a SerializationException as Cassini attempts to transfer the principal from one thread to another. This issue doesn't occur with IIS, because IIS doesn't switch threads like Cassini does.

Several of our unit tests for CSLA use custom principals, because we have tests for the various authentication modes supported by CSLA .NET for Silverlight - including the use of a custom principal object. These tests would sporadically fail on Cassini, but only under load. Apparently the problem would only manifest if we were able to get Cassini to recycle an existing thread off the thread pool.

In Eugene's post he suggests that the solution to dealing with faults/exceptions is to wrap your code in a try..catch block and return any exception information as part of your service contract. The CSLA data portal has always done this, and so we were initially puzzled by the continuing 404 errors. However, it turns out that Cassini was failing *before any of our code ran*. Thanks to this, we couldn't wrap a try..catch around the code, because it wasn't our code...

This gave us another clue though. It turns out that the issue we faced was that a request would put a custom principal on the server thread. That principal was never removed from the thread, and if that thread got recycled (by random chance) we'd get the SerializationException. The solution is to ensure that the thread principal is set to null as each server request completes. That way a recycled thread never has a custom principal.

Again, not an issue that affects IIS, but by figuring this out we're now able to use Cassini too, which is far more convenient.

I post all this, because if you encounter 404 errors in Silverlight 2, you should first follow Eugene's advice and return error details as part of your service contract (which can really alter your service design!). And if you do that and still have trouble, look to deeper issues with the web host or network stack, they can be devious...
