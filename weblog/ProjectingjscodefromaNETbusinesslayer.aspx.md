---
title: Projecting js code from a .NET business layer
postDate: 2013-02-14T10:39:23.1353801-06:00
abstract: 
postStatus: publish
---
14 February 2013

In a recent email thread I ended up writing a lengthy bit of content summarizing some of my thoughts around the idea of automatically projecting js code into an HTML 5 (h5js) browser app.

Another participant in the thread mentioned that he’s a strong proponent of separation of concerns, and in particular keeping the “model” separate from data access. In his context the “model” is basically a set of data container or DTO objects. My response:

-----------------------------

I agree about separation of concerns at the lower levels.

I am a firm believer in domain focused business objects though. In the use of “real” OOD, which largely eliminates the need for add-on hacks like a viewmodel.

In other words, apps should have clearly defined logical layers. I use this model:


> Interface
> Interface control
> Business
> Data access
> Data storage


This model works for pretty much everything: web apps, smart client apps, service apps, workflow tasks (apps), etc.

The key is that the business layer consists of honest-to-god real life business domain objects. These are designed using OOD so they reflect the requirements of the user scenario, not the database design.

If you have data-centric objects, they’ll live in the Data access layer. And that’s pretty common when using any ORM or something like EF, where the tools help you create data-centric types. That’s very useful – then all you need to do is use object:object mapping (OOM) to get the data from the data-centric objects into the more meaningful business domain objects.

At no point should any layer talk to the database other than the Data access layer. And at no point should the Interface/Interface control layers interact with anything except the Business layer.

Given all that, the question with smart client web apps (as I’ve taken to calling these weird h5js/.NET hybrids) is whether you are using a service-oriented architecture or an n-tier architecture. This choice must be made \_*first*\_ because it impacts every other decision.

The service-oriented approach says you are creating a system composed of multiple apps. In our discussion this would be the smart client h5js app and the server-side service app. SOA mandates that these apps don’t trust each other, and that they communicate through loosely coupled and clearly defined interface contracts. That allows the apps to version independently. And the lack of trust means that data flowing from the consuming app (h5js) to the service app isn’t trusted – which makes sense given how easy it is to hack anything running in the browser. In this world each app should (imo) consist of a series of layers such as those I mentioned earlier.

The n-tier approach says you are creating one app with multiple layers, and those layers might be deployed on different physical tiers. Because this is one app, the layers can and should have reasonable levels of trust between them. As a result you shouldn’t feel the need to re-run business logic just because the data flowed from one layer/tier to another (completely different from SOA).

N-tier can be challenging because you typically have to decide where to physically put the business layer: on the client to give the user a rich and interactive experience, or on the server for more control and easier maintenance. In the case of my CSLA .NET framework I embraced the concept of \_*mobile objects*\_ where the business layer literally runs on the client AND on the server, allowing you to easily run business logic where most appropriate. Sadly this requires that the same code can actually run on the client and server, which isn’t the case when the client and server are disparate platforms (e.g. h5js and .NET).

This idea of projecting server-side business domain objects into the client fits naturally into the n-tier world. This has been an area of deep discussion for months within the CSLA dev team – how to make it practical to translate the rich domain business behaviors into js without imposing a major burden of writing js alongside C#.

CSLA objects have a very rich set of rules and behaviors that ideally would be automatically projected into a js business layer for use by the smart client h5js Interface and Interface control layers. I love this idea – but the trick is to make it possible such that there’s not a major new burden for developers.

This idea of projecting server-side business domain objects into the client is a less natural fit for a service-oriented system, because there’s a clear and obvious level of coupling between the service app and the h5js app (given that parts of the h5js app literally generate based on the service app). I’m not sure this is a total roadblock, but you have to go into this recognizing that such an approach compromises the primary purpose of SOA, which is loose coupling between the apps in the system…
