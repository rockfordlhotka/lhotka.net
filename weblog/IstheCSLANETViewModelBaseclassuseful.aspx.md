---
title: Is the CSLA .NET ViewModelBase class useful?
postDate: 2014-10-24T13:21:06.7288309-05:00
abstract: 
postStatus: publish
---
24 October 2014

[CSLA .NET](http://www.cslanet.com/) predates the MVVM pattern by around a decade. All that time I've been telling people they should create an object model that matches the problem domain. Lots of people told me I was talking about "old fashioned OO" or otherwise dismissed what I was saying. They preferred to think of their 'model' as simple data container objects.

At some point most of them eventually realized that they needed *something*that actually matched the problem domain, and that their 'model' couldn't do it while still being simple data containers.

So they invented a new concept called a 'viewmodel' that (when done right) does match the problem domain - just like the UI always matches the problem domain.

At this point if you are a CSLA user you encounter an interesting situation, where you've been creating domain objects maybe for a decade longer than MVVM has existed, but MVVM is now the POTY (pattern of the year) and so you feel like you need to use it. Everyone wants the POTY after all :)

I spent a lot of time thinking about this and eventually decided that creating a viewmodel that echoes all your domain object's properties is just a lot of busy-work that has huge cost in development and testing. So it is \_far\_ better for your 'viewmodel' to just expose your preexisting CSLA domain objects to the UI, because THAT IS WHAT THEY ARE DESIGNED FOR.

Now it turns out that the MVVM pattern does have one thing CSLA doesn't have: the concept that the viewmodel implements UI-specific verbs (methods).

A good CSLA model is UI-neutral and so doesn't include methods for things like navigation or displaying error messages. A good viewmodel \_does\_ have methods that do those things through the use of an MVVM framework so those methods aren't implemented in a way that tightly couples the viewmodel to the UI technology.

Given that, combining CSLA with MVVM means that you need a viewmodel that exposes your CSLA domain objects to the UI, and that implements UI-specific methods to manage user interaction.

In the simple case what you need is a viewmodel class that exposes a single Model property, and then you can implement your UI handler methods. That's what ViewModelBase does for you.

In a lot of more complex scenarios you'll need a viewmodel that exposes multiple CSLA model objects - in which case you can learn from the way ViewModelBase is implemented and leverage that knowledge to create your own viewmodels. In any case though, the viewmodels implement properties to expose the CSLA domain objects to the UI and also implement methods that handle UI-specific requirements. The viewmodels shouldn’t be echoing the existing CSLA domain properties to the UI, because that’s just a waste of time, effort, and money.
