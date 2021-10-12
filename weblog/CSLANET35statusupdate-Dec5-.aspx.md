---
title: CSLA .NET 3.5 status update (Dec 5)
postDate: 2007-12-05T21:23:59.9136128-06:00
abstract: 
postStatus: publish
---
05 December 2007

There's been a lot of activity in CSLA .NET, moving toward version 3.5.

Aaron (my colleague at [<font color="#669966">Magenic</font>](http://www.magenic.com/)) has implemented indexed queries over CSLA collections in LINQ to Objects. So when you run a LINQ query against a CSLA collection (BusinessListBase, ReadOnlyListBase) and the where clause uses an indexed property the query will be much faster. You control which of your properties are indexed by using an attribute in the child business class on each property.

Aaron is now working on ensuring that non-projection queries against a CSLA collection result in a live updatable "view" of the original collection. Much like the way SortedBindingList and FilteredBindingList work today. So a non-projection query will not result in a simple, disconnected IEnumerable&lt;T&gt;, but will result in something richer and more natural to use.

In the meantime, I've been tackling items off the [<font color="#669966">wish list</font>](http://www.lhotka.net/cslanet/WishList.aspx). If you look at the list, you'll see quite a bit of green, indicating items that are (or will be) complete in 3.5.

Some highlights include:

- The code to declare a property has been reduced by more than 30% per property, and I've minimized the use of string literal property names for maintainability of code.
- Added a child management concept so parent objects can automatically manage their children so you don't have to override IsValid/IsDirty, cascading events or resetting edit levels when using lazy loading. The result is code that is smaller and more maintainable.
- SmartDate now supports type conversion, making it far easier to get values to/from string, DateTime and the new DateTimeOffset type.
- DataMapper now does much richer type coercion, using IConvertible and value converters if they exist (like they now do for SmartDate). This is just the start of the DataMapper enhancements - watch for more.
- A variety of small, but often important, changes and enhancements around validation rules and broken rules. These changes enable several important scenarios, especially around the consumption of broken rule data.

