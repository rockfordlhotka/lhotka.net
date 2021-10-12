---
title: Using the MVVM pattern requires a framework
postDate: 2012-05-07T15:01:55.8777382-05:00
abstract: 
postStatus: publish
---
07 May 2012

There are three fairly popular presentation layer design patterns that I collectively call the “M” patterns: MVC, MVP, and MVVM. This is because they all have an “M” standing for “Model”, plus some other constructs.

The thing with all of these “M” patterns is that for typical developers the patterns are useless without a framework. Using the patterns without a framework almost always leads to confusion, complication, high costs, frustration, and ultimately despair.

These are just patterns after all, not implementations. And they are big, complex patterns that include quite a few concepts that must work together correctly to enable success.

You can’t sew a fancy dress just because you have a pattern. You need appropriate tools, knowledge, and experience. The same is true with these complex “M” patterns.

And if you want to repeat the process of sewing a fancy dress over and over again (efficiently), you need specialized tooling for this purpose. In software terms this is a framework.

Trying to do something like MVVM without a framework is a huge amount of work. Tons of duplicate code, reinventing the wheel, and retraining people to think differently.

At least with a framework you avoid the duplicate code and hopefully don’t have to reinvent the wheel – allowing you to focus on retraining people. The retraining part is generally unavoidable, but a framework provides plumbing code and structure, making the process easier.

You might ask yourself why the MVC pattern only became popular in ASP.NET a few short years ago. The pattern has existed since (at least) the mid-1990’s, and yet few people used it, and even fewer used it successfully. This includes people on other platforms too, at least up to the point that those platforms included well-implemented MVC frameworks.

Strangely, MVC only started to become mainstream in the Microsoft world when ASP.NET MVC showed up. This is a comprehensive framework with tooling integrated into Visual Studio. As a result. typical developers can just build models, views, and controllers. Prior to that point they also had to build everything the MVC framework does – which is a lot of code. And not just a lot of code, but code that has absolutely nothing to do with business value, and only relates to implementation of the pattern itself.

We’re in the same situation today with MVVM in WPF, Silverlight, Windows Phone, and Windows Runtime (WinRT in Windows 8). If you want to do MVVM without a framework, you will have to build everything a framework would do – which is a lot of code that provides absolutely no direct business value.

Typical developers really do want to focus on building models, views, and viewmodels. They don’t want to have to build weak reference based event routers, navigation models, view abstractions, and all the other things a framework must do. In fact, most developers probably *can’t*build those things, because they aren’t platform/framework wonks. It takes a special kind of passion (or craziness) to learn the deep, highly specialized techniques and tricks necessary to build a framework like this.

What I really *wish* would happen, is for Microsoft to build an MVVM framework comparable to ASP.NET MVC. Embed it into the .NET/XAML support for WinRT/Metro, and include tooling in VS so we can right-click and add views and viewmodels. Ideally this would be an open, iterative process like ASP.NET MVC has been – so after a few years the framework reflects the smartest thoughts from Microsoft and from the community at large.

In the meantime, [Caliburn Micro](http://caliburnmicro.codeplex.com/) appears to be the best MVVM framework out there – certainly the most widely used. Probably followed by various implementations using PRISM, and then MVVM Light, and some others.
