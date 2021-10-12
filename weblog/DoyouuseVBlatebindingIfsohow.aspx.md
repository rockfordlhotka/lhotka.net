---
title: Do you use VB late binding? If so, how?
postDate: 2008-03-16T15:56:16.998-05:00
abstract: 
postStatus: publish
---
16 March 2008

I have a question (helping a colleague do some research) for all .NET VB developers.

Do you use late binding in VB? If so, how/why do you use it? What are the scenarios where you find it of value?

I'll start this off with my own observations:

I use late binding when getting data of a given shape from unknown types.

For example, you can write a nice bit of reusable data access code that accepts data from a web service, LINQ object, etc. by using late binding. You can’t easily do this without late binding in fact, because the *types of the objects are different* even though their shapes are the same.

That dynamic interface concept that got dropped from VB9 would address this issue in a better way, but late binding makes it work too.

I also use late binding when creating some generic types. There are cases where generics and casting are problematic, but converting a value to type Object first allows you to do a cast or operation that wouldn’t otherwise be allowed. I don’t know if this is “late binding” as such, but it is a useful technique!

I have used late binding when dynamically loading an assembly for interaction. Ideally you’d require the assembly author to implement one of your interfaces, but that’s not always possible, and late binding is a particularly nice way to get “polymorphic” access to multiple assemblies that you don’t control.

What about you?
