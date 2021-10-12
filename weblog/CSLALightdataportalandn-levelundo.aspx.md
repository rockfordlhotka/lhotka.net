---
title: CSLA Light data portal and n-level undo
postDate: 2008-06-24T23:24:09.078-05:00
abstract: 
postStatus: publish
---
24 June 2008

With serialization largely out of the way - or at least under control - as described in a recent blog post, we've been able to put some focus on a couple other key areas.

#### N-Level Undo

The n-level undo functionality in CSLA .NET relies on reflection against private fields. Obviously that's not possible in Silverlight. Fortunately the serialization scheme we're using means that there's already a mechanism for trapping the values stored in the field manager. And there's the OnGetState()/OnSetState() methods that allow a business developer to trap/restore values in their private fields (if they choose). So UndoableBase had to be altered to use these techniques rather than using reflection. The end result is the same, which is what really matters.

We opted not to replicate IEditableObject into CSLA Light. It is a .NET interface used by Windows Forms data binding, and is the source of never-ending pain thanks to all the edge cases and idiosyncrasies around this, seemingly simple, interface. Of course the interface isn't used by Silverlight (or WPF), and so isn't necessary. The effect of this choice is to simplify quite a bit of the n-level undo code, while at the same time preserving the shape of the pre-existing *public* interface for all objects. In other words, BeginEdit(), CancelEdit() and ApplyEdit() work as expected, but you can't use IEditableObject to get at its versions of those methods.

Justin just ran into a strange issue with BusinessListBase, where an attempt to iterate through the items in the list caused a strange runtime exception from somewhere deep in the bowels of the Silverlight runtime. It appears there's some issue with a subclass of a collection iterating through its own items in a foreach loop. A for loop works fine however, so we have a workaround.

Ultimately however, the ability to easily implement a Cancel button, including when using modal dialogs (which can be simulated in Silverlight) is supported

#### Data Portal

The data portal is coming along pretty well too. It supports a provider model, conceptually similar to the data portal in .NET. And we currently have two providers: local and WCF.

One issue we're facing here is that Silverlight has no configuration subsystem comparable to System.Configuration. So there's no easy way to get configuration data from an "app.config" file or equivalent. At the moment I've come up with a code-based configuration scheme - but (unless Microsoft puts out a solution soon) we'll probably end up creating some embedded resource-based configuration subsystem of our own.

The data portal itself is asynchronous. This changes the way the UI code interacts with the data portal when compared to .NET code. Rather than just calling DataPortal.Fetch() to get an object, in Silverlight the UI must call a BeginFetch() method to start the process and handle a completed event to process any results when they return.

This means the UI code looks something like this:


> <font face="Courier New" size="2">var dp = new DataPortal&lt;MockEditableRoot&gt;();<br>dp.FetchCompleted += new EventHandler&lt;DataPortalResult&lt;MockEditableRoot&gt;&gt;(dp_FetchCompleted); <br>dp.BeginFetch();</font>


This code starts the process, and the dp\_FetchCompleted is invoked (on the UI thread) when the call is complete:


> <font face="Courier New" size="2">private void dp_FetchCompleted(object sender, DataPortalResult&lt;MockEditableRoot&gt; e)<br>{<br>&nbsp; this.DataContext = e.Object;<br>}</font>


Alternately you can wrap this code into a factory method and completed event provided by the business class. That is a little closer to the typical CSLA .NET model - but is still async, and the UI still must handle the result in a callback event handler.

##### Local Data Portal

When using the data portal in local mode, it calls DataPortal\_XYZ methods, much like the .NET data portal. There are a couple interesting differences however. The first being that the DataPortal\_XYZ methods must be public in scope. Remember, no private reflection, so only public methods can be called.

I debated about using an interface-based approach, but decided against it for a couple reasons. First, it would be dissimilar to the existing .NET approach. Second, it would mean that your DataPortal\_XYZ methods couldn't be strongly typed - they'd have to accept parameters of type object and you'd have to cast them to something meaningful.

The second difference flows from the fact that most server-related activities in Silverlight are asynchronous. Most DataPortal\_XYZ methods, therefore, will be invoking async server calls and getting the results from a callback event. So all DataPortal\_XYZ methods are provided a delegate they can use to do a callback to indicate completion. In a simple (synchronous) example it looks like this:


> <font face="Courier New" size="2">public void DataPortal_Insert(<br>&nbsp; Csla.DataPortalClient.LocalProxy&lt;MockEditableRoot&gt;.CompletedHandler handler)<br>{<br></font><font face="Courier New" size="2">&nbsp; LoadProperty&lt;string&gt;(DataPortalMethodProperty, "insert");<br>&nbsp; handler(this, null);<br>} </font>


The DataPortal\_Insert() method accepts a CompletedHandler parameter it can use to indicate completion. The call to handler() is the completion call, and the first parameter is the resulting business object, while the second is an Exception object if you want to indicate failure.

In an *asynchronous* example things are a bit more complex. And the async scenario is the most common. Typically when using a "local" data portal you'd be doing so because you want to call some web service or data service from Silverlight. And since all the server call technologies in Silverlight are async, your DataPortal\_XYZ method will almost certainly be invoking some async service. So more normal code might look like this:


> <font face="Courier New" size="2">public void DataPortal_Insert(<br>&nbsp; Csla.DataPortalClient.LocalProxy&lt;MockEditableRoot&gt;.CompletedHandler handler)<br>{<br></font><font face="Courier New" size="2">&nbsp; var svc = new Csla.Testing.Business.TestService.TestServiceClient();<br>&nbsp; svc.InsertDataCompleted += <br>&nbsp;&nbsp;&nbsp; new EventHandler&lt;Csla.Testing.Business.TestService.InsertDataCompletedEventArgs&gt;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (svc_InsertDataCompleted);<br>&nbsp; svc.InsertData(GetProperty&lt;string&gt;(DataPortalMethodProperty), handler);<br>} </font>
>
> <font face="Courier New" size="2">void svc_InsertDataCompleted(<br>&nbsp; object sender, Csla.Testing.Business.TestService.InsertDataCompletedEventArgs e)<br>{<br>&nbsp; var handler = (Csla.DataPortalClient.LocalProxy&lt;MockEditableRoot&gt;.CompletedHandler)e.UserState;<br>&nbsp; handler((MockEditableRoot)e.Result, e.Error);<br>} </font>


This looks a bit odd, but after you do a bit of Silverlight programming this pattern becomes second nature.

The DataPortal\_XYZ method sets up and starts the call - passing parameters to the service, and one parameter that is "user state", which is extra (doesn't go to the server, but stays on the client). Notice that before making the InsertDataAsync() call, which is the call to the service, the code hooks the InsertDataCompleted event - this is the event that will be raised (on the UI thread) when the service call completes.

The svc\_InsertDataCompleted() method is the event handler. This is where you write the code to handle the results from the service call. When using the data portal, this is where you call back into CSLA to indicate that the call is complete. Ultimately CSLA will return the result to the UI code, but this mechanism allows CSLA to do any extra processing between the DP\_XYZ call and the UI so it can manage the state of your business object.

You can also shrink this by using a lambda:


> <font face="Courier New" size="2">public void DataPortal_Insert(<br>&nbsp; Csla.DataPortalClient.LocalProxy&lt;MockEditableRoot&gt;.CompletedHandler handler)<br>{<br></font><font face="Courier New" size="2">&nbsp; var svc = new Csla.Testing.Business.TestService.TestServiceClient();<br>&nbsp; svc.InsertDataCompleted += (o, e) =&gt; { handler((MockEditableRoot)e.Result, e.Error); };<br>&nbsp; svc.InsertDataAsync(GetProperty&lt;string&gt;(DataPortalMethodProperty));<br>} </font>


That eliminates the need for a separate event handler method and simplifies the code.

##### Remote Data Portal

The remote data portal option works very much like the normal .NET data portal, and is generally simpler to use that the local data portal. When the data portal is configured to use the WcfProxy, it will use WCF to communicate with a CSLA .NET data portal on the web/app server.

In this scenario you need a web or app server that is hosting a CSLA .NET data portal - the .NET end of the CSLA Light data portal. The CSLA Light code running on the Silverlight client will call the CSLA .NET code running on the app server.

When using a remote data portal, the Silverlight business object *will not include any DataPortal\_XYZ methods*. The DataPortal\_XYZ methods will only be implemented in the .NET code, and will only exist on the server. The client-side code will still call the data portal, but the call will be automatically routed through WCF to the app server.

This is exactly the same kind of behavior you'd get from the existing .NET data portal - you can choose to use a local or remote data portal, but the business object and UI code are the same either way (with the exception that a local data portal requires implementation of DataPortal\_XYZ methods).

On the app server, which is running CSLA .NET, requests will come in from the Silverlight client. These requests can be handled in one of two ways.

The default is for the client call to be routed into the CSLA .NET data portal, and the rest of the processing is normal CSLA .NET processing. In other words, a Silverlight Fetch() call results in a DataPortal.Fetch() call on the app server, which runs the DataPortal\_Fetch() method just like it always has. The result of the data portal call on the app server is then returned to the Silverlight client.

I call that the "pass-through" mode because the server-side data portal just passes the client call through to the "real" data portal. And this is a great option for when you trust the client that is running the Silverlight app, because it requires the least amount of code and provides the simplest solution.

But if you don't trust the Silverlight client. If you are worried that someone will break into the Silverlight runtime and somehow put bad data into your object's fields (perhaps bypassing your business logic, etc), then extra precautions are required. To address that concern, the server-side data portal can optionally invoke an "observer" or "factory" (I'm still debating the name of this thing).

To do this, on your server-side business object code (in the server-only partial class) you use the MobileFactory attribute to specify the type name of the factory object, and the method names to be called for create, fetch, update and delete operations (the only operations the data portal supports).


> <font face="Courier New" size="2">[MobileFactory("MyProject.MyFactory, MyProject", "Create", "Fetch", "Update", "Delete")]<br>public partial class MockEditableRoot</font>


Then you must implement the factory class:


> <font face="Courier New" size="2">public class MyFactory<br>{<br>&nbsp; public object Create(object criteria)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; // create, initialize and return new object here<br>&nbsp; }<br><br>&nbsp; public object Fetch(object criteria)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; // create, load and return object here&nbsp; <br>&nbsp; }<br><br>&nbsp; public object Update(object inbound)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; // insert, update or delete object here<br>&nbsp;&nbsp;&nbsp; // return resulting object<br>&nbsp; }<br><br>&nbsp; public void Delete(object criteria)<br>&nbsp; {<br>&nbsp;&nbsp;&nbsp; // delete object here&nbsp; <br>&nbsp; }<br>}</font>


The criteria or business object from the client does materialize on the server. Of course on the server it materializes within *code you control*, and so you can safely interact with the object from within the methods of this factory. Here, you can force re-running of the validation rules, apply extra authorization rules or other processing you see fit - all on the app server. Only if you are happy with the object would you then invoke the "real" data portal to actually allow the persistence to occur.
