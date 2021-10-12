---
title: Some thoughts on Application Architecture
postDate: 2010-08-22T10:55:06.472646-05:00
abstract: 
postStatus: publish
---
22 August 2010

My personal area of focus is on application architecture, obviously around the .NET platform, though most of the concepts, patterns and techniques apply to any mature development platform.

Application architecture is all about defining the standards, practices and patterns that bring consistency across all development efforts on a platform. It is not the same as application design – architecture spans applications, while design is applied to every specific application. Any relevant architecture will enable a broad set of applications, and therefore must enable multiple possible designs.

It is also the case that application architecture, in my view, includes “horizontal” and “vertical” concepts.

Horizontal concepts apply to any and all applications and are largely orthogonal to any specific application design. These concepts include guidelines around authentication, authorization, integration with operational monitoring systems, logging, tracing, etc.

Vertical concepts cover the actual shape of applications, including concepts like layered application structure, what presentation layer design patterns to use (MVC, MVVM, etc), how the presentation layer interacts with the business layer, how the business layer is constructed (object-oriented, workflow, function libraries, etc), how the data access layer is constructed, whether broad patterns like DI/IoC are used and so forth.

In today’s world, an application architecture must at least encompass the possibility of n-tier and service-oriented architectures. Both horizontal and vertical aspects of the architecture must be able to account for n-tier and SOA application models, because both of these models are required to create the applications necessary to support any sizable suite of enterprise application requirements.

It is quite possible to define application architectures at a platform-neutral level. And in a large organization this can be valuable. But in my view, this is all an academic (and essentially useless) endeavor unless the architectures are taken to another level of detail specific to a given platform (such as .NET).

This is because the architecture must be actually relevant to on-the-ground developers or it is just so much paper. Developers have hard goals and deadlines, and they usually want to get their work done in time to get home for their kid’s soccer games. Abstract architectures just mean more reading and essentially detract from the developers’ ability to get their work done.

Concrete architectures *might be helpful* to developers – at least there’s some chance of relevance in day to day work.

But to really make an architecture relevant, the architect group must go beyond concepts, standards and guidelines. They need to provide tools, frameworks and other tangible elements that *make developer’s lives easier*.

Developers are like electricity/water/insert-your-analogy-here, in that they take the path of least resistance. If an architecture makes things harder, they’ll bypass it. If an architecture (usually along with tools/frameworks/etc) makes things easier, they’ll embrace it.

Architecture by itself is just paper – concepts – nothing tangible. So it is virtually impossible for *architecture* to make developer’s lives easier. But codify an architecture into a framework, add some automated tooling, pre-built components and training – and all of a sudden it becomes easier to do the right thing by following the architecture, than by doing the wrong thing by ignoring it.

This is the recipe for winning when it comes to application architecture: be pragmatic, be comprehensive and above all, make sure the easiest path for developers is the right path – the path defined by your architecture.
