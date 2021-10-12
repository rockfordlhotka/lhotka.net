---
title: Prototype Silverlight data portal
postDate: 2008-04-23T09:08:36.275-05:00
abstract: 
postStatus: publish
---
23 April 2008

I spent some time over the past few days using my prototype Silverlight serializer to build a prototype Silverlight data portal. It is still fairly far from complete, but at least I've proved out the basic concept and uncovered some interesting side-effects of living in Silverlight.

The good news is that the basic concept of the data portal works. Defining objects that physically move between the Silverlight client and a .NET web server is practical, and works in a manner similar to the pure .NET data portal.

The bad news is that it can't work *exactly* like the pure .NET data portal, and the technique does require some manual effort when creating the business assemblies (yes, plural).

The approach I'm taking involves having two business assemblies (VS projects) that share many of the same code files. Suppose you want to have a Person object move between the client and server. You need Person in a Silverlight class library *and in a .NET class library*. This means two projects are required, even if they have the same code file.

Visual Studio makes this reasonable, because you can create the file in one project (say the Silverlight class library) and then Add Existing Item and use the *Link* feature to get that same file included into a .NET class library project.

I also make the class be a partial class, so I can add extra code to the .NET class library implementation. The result is:


> BusinessLibrary.Client (Silverlight class library)
>   -&gt; Person.cs
>
> BusinessLibrary.Server (.NET class library)
>   -&gt; Person.cs (linked from BusinessLibrary.Client)
>   -&gt; Person.Server.cs


One key thing is that *both projects build a file called BusinessLibrary.dll*. Also, because Person.cs is a shared file, it obviously has the same namespace. This is all very important, because the serializer requires that the fully qualified type name ("namespace.type,assembly") be the same on client and server. In my case it is "BusinessLibrary.Person,BusinessLibrary".

The Person.Server.cs file contains the server-only parts of the Person class - it is just the rest of the partial class. The only catch here is that it *can not define any fields* because that would obviously confuse the serializer since those fields wouldn't exist on the client. Well, actually it could define fields as long as they were marked as NonSerialized.

Of course you could also have a partial Person.Client.cs in the Silverlight class library - though I haven't found a need for that just yet.

One thing I'm debating is whether the .NET side of the data portal should just directly delegate Silverlight calls into the "real" data portal - effectively acting as a passive router between Silverlight and the .NET objects. OR the .NET side of the data portal could invoke specific methods (like Silverlight\_Create(), Silverlight\_Update(), etc) so the business developer can include code to decide whether the calls should be processed on the server at all.

The first approach is simple, and certainly makes for a compelling story because it works very much like CSLA today. The Silverlight client gets/updates objects in a very direct manner.

The second approach is a little more complex, but might be better because I'm not sure you should blindly trust anything coming from the Silverlight client. You can make a good argument that Silverlight is always outside the trust boundary of your server application, so blindly passing calls from the client through the data portal may not be advisable.

Either way, what's really cool is that the original .NET data portal *remains fully intact*. This means that the following two physical deployment scenarios are available:


> Silverlight -&gt; Web server -&gt; database
> Silverlight -&gt; Web server -&gt; App server -&gt; database


Whether the web/app server is in 2- or 3-tier configuration is just a matter of how the original .NET data portal (running on the web server) is configured. I think that's awesome, as it easily enables two very common web server configurations.

The big difference in how the Silverlight data portal works as compared to the .NET data portal is on the client. In Silverlight you should never block the main UI thread, which means calls to the server should be asynchronous. Which means the UI code can't just do this:


> var person = Person.GetPerson(123);


That sort of synchronous call would block the UI thread and lock the browser. Instead, my current approach requires the UI developer to write code like this:


> var dp = new Csla.DataPortal();
> dp.FetchCompleted +=
>   new EventHandler&lt;Csla.DataPortalResult&lt;Person&gt;&gt;(dp\_FetchCompleted);
> dp.BeginFetch&lt;Person&gt;(new SingleCriteria&lt;int&gt;(123));


with a dp\_FetchCompleted() method like:


> private void dp\_FetchCompleted(object sender, Csla.DataPortalResult&lt;Person&gt; e)
> {
>   if (e.Error != null)
>     // e.Error is an exception - deal with the issue
>   else
>     // e.Object is your result - use it
> }


So the UI code is more cumbersome than in .NET, but it follows the basic service-calling technique used in any current Silverlight code, and I don't think it is too bad. It isn't clear how to make this any simpler really.
