---
title: CSLA .NET 3.8 Beta 2 MVVM support
postDate: 2009-10-25T23:23:04.9677354-05:00
abstract: 
postStatus: publish
---
25 October 2009

I’ve blogged about MVVM several times over the past few months. If you watch my posts you’ll see that I started out pretty skeptical of the pattern, and then worked through it trying to find the shiny silver lining that was promised.

One of the biggest challenges with patterns is that people expect them to be a recipe, when in reality they are just a vague formalization of a concept. Just look at MVC, an incredibly mature pattern, and all the radically different ways it gets implemented (for better or often worse) in applications. While MVVM isn’t nearly as mature as MVC, it turns out that it really is a good concept – when “applied correctly”.

In my view a pattern should only be used if its positive consequences outweigh its negative consequences. Many patterns, oddly enough, require extra code and/or configuration over what you’d normally write – which is a negative consequence. And in some interpretations of MVVM this is very much the case – which was the primary reason for my initial skepticism.

On the other hand, with some thought, foresight and work it is often possible to mitigate some of the more negative consequences of many of the more popular patterns. This turns out to be absolutely true for MVVM.

To me, the real sweet spot for a pattern is if it can provide its positive consequences with little or no negative impact at all.

My time with CSLA .NET 3.8 has been divided into just a few areas:

- Bug fixes (minor)
- DataAnnotations (minor – but really nice)
- Silverlight 3 element binding (major – also really nice)
- MVVM support (major – and very cool)


In the end, I think I’ve got something that enables the use of the MVVM design pattern, probably in several variations, to work swimmingly with CSLA .NET. I’ll go so far as to say that I think this implementation of MVVM makes developing Silverlight and WPF apps *easier* than out-of-the-box coding (drag-and-drop, handling UI events, using data provider controls). And by easier I mean no more code, often less code, and easier to read/test/maintain code. So the pattern is purely helpful, with no negative consequences of note. Exactly what you’d hope for.

What does this look like?

**CSLA .NET MVVM Support**

First, you must realize that CSLA .NET helps you create what’s called a *rich model* as opposed to various other technologies (like Add Service Reference) that help you create an *anemic model*. Using MVVM with an anemic model is useful, but can require a lot of work, because your viewmodel object needs to compensate for all the stuff the model doesn’t do. But with a rich model, the viewmodel requires far less work because the model is already first-class citizen.

To this end, CSLA .NET provides some helper types that you may optionally use to enable a rich model MVVM implementation. At the same time, I fully recognize that many (most?) people will find/build and use an MVVM UI framework, so the CSLA .NET helper types can be used individually, all together or not at all – as you choose.

Two parts of MVVM already (mostly) exist if you are using CSLA .NET and Silverlight or WPF. CSLA .NET helps you create business domain objects that are your Model, and XAML helps you create your View (with a little help). So in my mind those are essentially a given. What’s left is the need to create the ViewModel.

Notice that I said XAML gives you the view – *with a little help*. This is because WPF commanding isn’t quite enough to do MVVM, and Silverlight doesn’t even have commanding. So the “little help” is something that handles arbitrary UI events and transforms them into arbitrary method calls on the DataContext (presumably your viewmodel). I would expect any decent MVVM UI framework to solve this most basic problem, and of course they do. Sadly there’s no standard solution, so each UI framework does their own thing.

**View Event Handling**

While not a UI framework, CSLA .NET does provide a basic solution to this one critical problem with using XAML to create a view. In fact it provides *two solutions*: InvokeMethod and Execute.

InvokeMethod is an attached property that understands how to handle an arbitrary UI event and to call an arbitrary method on the DataContext when that event is raised. As an attached property, you can attach it to any UIElement (FrameworkElement in Silverlight) to handle any event to call any method on the DataContext. Here’s a simple example:


> &lt;Button Content=”Save”
>             csla:InvokeMethod.TriggerEvent=”Click”
>             csla:InvokeMethod.MethodName=”SaveData” /&gt;


Execute is similar, but relies on the Blend 3 System.Windows.Interactivity event trigger concept to detect that the event was raised:


> &lt;Button Content="Save"&gt;
>   &lt;i:Interaction.Triggers&gt;
>     &lt;i:EventTrigger EventName="Click"&gt;
>       &lt;csla:Execute MethodName="SaveData" /&gt;
>     &lt;/i:EventTrigger&gt;
>   &lt;/i:Interaction.Triggers&gt;
> &lt;/Button&gt;


The advantage of using InvokeMethod is that it has several options around data binding that simply aren’t available to a trigger action like Execute. Most notably, InvokeMethod has a MethodParameter property that can be bound using a binding expression – so it can pull values from other UI controls, resources, the DataContext, etc. There’s no way to do this with a trigger action like Execute.

The advantage of using Execute is that trigger actions are something the Blend 3 designer understands. So InvokeMethod pretty much requires typing XAML, while Execute integrates more naturally into the Blend design experience.

In either case, the method on your viewmodel looks like this:


> public void SaveData()
> {
> }


Or this:


> public void SaveData(object sender, ExecuteEventArgs e)
> {
> }


Either one is fine, as InvokeMethod and Execute will work with either method signature. If you use the second option, the args parameter contains information about the control the raises the event, the event’s args and an optional MethodParameter value.

**Creating a ViewModel**

When using a rich model, I believe that a good viewmodel object will expose the model as a property, so the View can bind directly against the Model *and still have access to the viewmodel*. This way the viewmodel can extend and enhance the model without any extra effort. This works particularly well if the model already understands data binding – which is one of the primary features of CSLA .NET.

CSLA .NET includes ViewModelBase&lt;T&gt; and ViewModel&lt;T&gt;, both of which are base classes designed to make it easy to build a viewmodel for a CSLA .NET business object.

ViewModelBase has a public Model property, a handful of other useful public properties (like CanSave), and a whole bunch of protected methods. Again, my assumption is that many people will use some MVVM UI framework, and that framework will have its own constraints on how public methods must be implemented for their particular “commanding equivalent” functionality. The ViewModelBase class allows you to create public methods matching your UI framework’s requirements, but you can usually just delegate those calls to existing protected methods that do most of the work. These methods include:


| DoRefresh | (WPF only) Synchronously invokes a static factory method to create/fetch the Model. |
| --- | --- |
| BeginRefresh | Asynchronously invokes a static factory method to create/fetch the Model. |
| DoSave | (WPF only) Synchronously saves the Model (if it is a root object). |
| BeginSave | Asynchronously saves the Model (if it is a root object). |
| AddItem | Adds an item to the collection (if the Model is a BusinessListBase). |
| Remove | Removes an item from the collection (if the Model is a BusinessListBase). |
| Delete | Marks the Model for deletion (if the Model is a root BusinessBase). |
| Cancel | Cancels any changes that have been made to the Model (if ManageObjectLifetime is true). |


ViewModel is a subclass of ViewModelBase that implements public methods for use by InvokeMethod and/or Execute. If you use InvokeMethod/Execute, then you’ll want to create your viewmodel objects by subclassing ViewModel:


> public class CustomerViewModel : ViewModel&lt;Customer&gt;
> {
>   public CustomerViewModel()
>   {
>     BeginRefresh(“NewCustomer”);
>   }
> }


In many cases the constructor is all you’ll need to write, since the ViewModel&lt;T&gt; base class already implements the methods necessary to build a standard data entry form.

Again, if you are using an MVVM UI framework, you’ll probably want to create your own base class, somewhat like ViewModel&lt;T&gt;, by subclassing ViewModelBase&lt;T&gt; and implementing your public methods to match the requirements of the UI framework. You can use the code in ViewModel&lt;T&gt; as an example of how to do this.

I should also point out that the Model property is bindable. This means you can create “child viewmodel” objects that get their Model value by being bound to the property of some “parent viewmodel” or parent model. For example, you might have a form for working with SalesOrder objects, so your top level viewmodel exposes a SalesOrder object through its Model property. The following would be the XAML to set up the viewmodel for the form:


> &lt;UserControl.Resources&gt;
>   &lt;this:SalesOrderViewModel x:Key="ViewModel" /&gt;
> &lt;/UserControl.Resources&gt;
> &lt;Grid Name=”LayoutRoot” DataContext=”{Binding Source={StaticResource ViewModel}}”&gt;


Now you could just bind the detail region of the form (where you show the line items) to the LineItems property of the business object, and that works fine.

But suppose you want to bind a button or hyperlink control to an AddItem() method so the user can add items to the LineItems collection. How do you do that without writing code? The answer is that you set up a viewmodel (probably LineItemsViewModel) for that child region of the form, and you have the Model property of LineItemsViewModel bound to the LineItems property of the SalesOrder business object. In the child region you’d do something like this:


> &lt;Grid Name=”ChildRegionContainer”&gt;
>   &lt;Grid.Resources&gt;
>     &lt;this:LineItemsViewModel x:Key=”LineItemsViewModel”
>                                            Model=”{Binding Path=Model.LineItems}”/&gt;
>   &lt;/Grid.Resources&gt;
>   &lt;Grid Name=”ChildRegion” DataContext=”{Binding Source={StaticResource LineItemsViewModel}}”&gt;


The advantage of this is that any controls inside the ChildRegion grid can invoke methods on LineItemsViewModel – such as AddItem() or Remove() to add and remove items from the collection – all with no coding on your part.

**Creating the Model**

This is the part where I just smile. Because you already have the model if you used CSLA .NET and good object-oriented design to build your business domain objects. The same business objects you may already be using for Windows Forms or Web Forms will almost certainly just work in your WPF or Silverlight application (assuming you are using CSLA .NET 3.5 or higher – and can upgrade to CSLA .NET 3.8).

The primary goal of CSLA .NET, first and foremost, is to enable you to create a business layer that encapsulates your business, validation and authorization logic into a set of business domain objects. By doing so, you end up with a formal business layer on top of which you can build Silverlight, WPF, ASP.NET MVC, Web Forms, Windows Forms, asmx service or WCF service interfaces.

So the whole point of having this business layer is that when something like XAML comes along all you need to worry about is how to rebuild the UI, possibly using MVVM. But you *don’t* need to worry about rebuilding the business layer, or the data access layer or the database.

I’m pretty happy with the way CSLA .NET 3.8 enables the MVVM design pattern in Silverlight and WPF. As I said to start with, you’d hope that a pattern gives you positive consequences with little or no downside. With the support of InvokeMethod, Execute, ViewModelBase and ViewModel I think CSLA .NET makes MVVM meet that goal. And in fact, I think it allows you to build a UI with *less code* than many, seemingly simpler, alternatives.
