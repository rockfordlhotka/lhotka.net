---
title: Adding DataContextChanged in Silverlight
postDate: 2009-07-31T16:41:57.9038216-05:00
abstract: 
postStatus: publish
---
31 July 2009

There’s no DataContextChanged event in Silverlight. And that’s a serious problem for creating certain types of control, because sometimes you just need to know when your data context has been changed!

In my case I have the Csla.Silverlight.PropertyStatus control, which listens for events from the underlying data context object so it knows when to refresh the UI. If the data context changes, PropertyStatus needs to unhook the events from the old object, and hook the events on the new object. That means knowing when the data context has changed.

In version 3.6 we implemented a Source property and required that the data source be explicitly provided. That was unfortunate, but since it was our own property we could detect when the value was changed.

I recently did a bunch of research into this topic, trying to find a better answer. I’d rather hoped that Silverlight 3 would provide an answer, but no such luck…

It turns out that there’s a <strike>hack</strike> solution that does work. Actually there are a few, but most of them seem terribly complex, and this one seems somewhat easier to follow.

The basic idea is to create a data binding connection between your DataContext property and another of your properties. Then when DataContext changes, data binding will change your property, and you can detect that your property has changed. Rather a hack, but it works.

In its distilled form, the structure looks like this. First there’s the control class, which inherits from some framework base class:


> public class PropertyStatus : ContentControl
> {


Then there’s the constructor, which includes a handler for the Loaded event, which is where the real magic occurs:


> public PropertyStatus()
> {
>   Loaded += (o, e) =&gt;
>   {
>     var b = new System.Windows.Data.Binding();
>     this.SetBinding(SourceProperty, b);
>   };
> }


When the control is loaded, a new Binding object is created. This Binding object picks up the default DataContext value. The Source property is then bound to this new Binding, which effectively binds it to the default DataContext. Definitely a bit of hackery here…

Obviously this means there’s a Source property – or at least the shell of one. I don’t really want a visible Source property, because that would be confusing, but I must at least implement the DependencyProperty as a public member:


> public static readonly DependencyProperty SourceProperty = DependencyProperty.Register(
>   "Source",
>   typeof(object),
>   typeof(PropertyStatus),
>   new PropertyMetadata((o, e) =&gt; ((PropertyStatus)o).SetSource(e.OldValue, e.NewValue)));


I do have a private Source property, though I’ve never found that it is invoked (breakpoints in the get/set blocks are never hit):


> private object Source
> {
>   get { return GetValue(SourceProperty); }
>   set
>   {
>     object old = Source;
>     SetValue(SourceProperty, value);
>     SetSource(old, value);
>   }
> }


The lambda in the static DependencyProperty declaration calls SetSource(), and this is my “data context changed” notification:


> private void SetSource(object old, object @new)
> {
>   DetachSource(old);
>   AttachSource(@new);
> ...
> }


I suppose this could be generalized into a base class, where SetSource() really raises a DataContextChanged event. I didn’t find the need for that, as I’ve only got a couple controls that need to know the data context has changed, and they inherit from different framework base classes.

The point being, with a little data binding hackery, it is not terribly hard to implement a method that is invoked when the data context changes. Not as nice as having the actual event like in WPF, but much nicer than forcing the XAML to explicitly set some data source property on every control.

(for those interested, this will be changed in CSLA .NET 3.7.1, and it will be a breaking change because the Source property will go away)
