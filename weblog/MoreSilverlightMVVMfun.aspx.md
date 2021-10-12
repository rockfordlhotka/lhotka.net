---
title: More Silverlight MVVM fun
postDate: 2009-09-02T16:25:26.1621062-05:00
abstract: 
postStatus: publish
---
02 September 2009

I keep plucking away at the MVVM ideas, trying to make sure CSLA .NET allows people to implement the pattern in a smooth manner.

But I keep fighting with UI stuff in the process…

My scenarios center around the ListBox, because I find it to be nicely problematic. And common. Most apps have lists of stuff, and users select n items from the list and then do something with the items. So single-select and multi-select ListBox scenarios, where actions are triggered by the selection changing, or when a button is clicked – this is my current problem domain. Pure UI stuff.

I updated my existing InvokeMethod component to solve these problems, with some challenges, but it works nicely to invoke a method on a ViewModel. I’ve also played with the EventTrigger concepts from Blend 3, creating an Execute trigger action that invokes a method on the ViewModel, but there are some serious limitations here.

One scenario is pretty easy – triggering an action from the SelectionChanged event of the ListBox itself. The InvokeMethod and Execute solutions can both be handled with zero code-behind – just XAML interacting with the ViewModel.

#### Single-select with InvokeMethod

With InvokeMethod it looks like this:


> &lt;ListBox ItemsSource="{Binding Path=Model}"
>          ItemTemplate="{StaticResource DataList}"
>          Name="DataListBox"
>          csla:InvokeMethod.Target="{Binding Source={StaticResource ListModel}}"
>          csla:InvokeMethod.TriggerEvent="SelectionChanged"
>          csla:InvokeMethod.MethodName="ShowItem"
>          csla:InvokeMethod.MethodParameter="{Binding RelativeSource={RelativeSource Self}, Path=SelectedItem}" /&gt;


And the ViewModel has a ShowItem() method like this:


> public void ShowItem(Data methodParameter)
> {
>   // process methodParameter
> }


Very simple and easy, and I like it a lot – except that InvokeMethod is fairly verbose and isn’t supported by Blend. I do like that the selected item is passed into the method as a strongly typed parameter though.

#### Single-select with event trigger

Using the event trigger model (which is supported by Blend) the ListBox looks like this:


> &lt;ListBox ItemsSource="{Binding Path=Model}"
>          ItemTemplate="{StaticResource DataList}"
>          SelectedItem="{Binding Path=SelectedData, Mode=TwoWay}"
>          Name="DataListBox"&gt;
>   &lt;i:Interaction.Triggers&gt;
>     &lt;i:EventTrigger EventName="SelectionChanged"&gt;
>       &lt;csla:Execute MethodName="ShowItem2" /&gt;
>     &lt;/i:EventTrigger&gt;
>   &lt;/i:Interaction.Triggers&gt;
> &lt;/ListBox&gt;


Notice that the ListBox.SelectedItem property is now bound to the SelectedData ViewModel property:


> public static readonly DependencyProperty SelectedDataProperty =
>     DependencyProperty.Register("SelectedData", typeof(Data), typeof(DataListViewModel), new PropertyMetadata(null));
> public Data SelectedData
> {
>   get { return (Data)GetValue(SelectedDataProperty); }
>   set { SetValue(SelectedDataProperty, value); OnPropertyChanged("SelectedData"); }
> }


And the ViewModel method looks like this:


> public void ShowItem2(object sender, Csla.Silverlight.ExecuteEventArgs e)
> {
>   // process this.SelectedData
> }


While this is supported by Blend, I dislike the fact that the command method (ShowItem2()) has an invisible side-effect in that it requires the SelectedData property to be set before it will work. No one could know this without looking at the code or at documentation, so the overall readability is reduced in my opinion.

However, both solutions end up with a ShowItem() method that has the strongly-typed selected item, and the XAML uses binding to interact with the ViewModel in a reasonably clean manner – so I think either way is perfectly acceptable.

#### Multi-select with InvokeMethod

The multi-select ListBox scenario requires a Button (or similar control). The user selects multiple items in the ListBox, then clicks the Button to trigger processing of those items.

This scenario is not nearly so nice. Partly this is because of the way the ListBox works I think (or binding). The problem is that the SelectedItems property of the ListBox returns an ObservableCollection&lt;object&gt;, and when a binding is established between SelectedItems and another property it gets a reference to a collection *that is not the collection you ultimately want*.

In other words, when the form loads, SelectedItems points to an empty collection, and anything bound to it gets connected to that collection. When items are later selected the SelectedItems property seems to end up pointing to a *different collection*, and the binding has no idea this happened. The binding is still pointing to the original empty collection.

This means the binding to SelectedItems must be refreshed *at the time the event trigger occurs*, such as the Button control’s Click event.

I made InvokeMethod take care of this, so when using InvokeMethod the ListBox looks like this:


> &lt;ListBox ItemsSource="{Binding Path=Model}"
>          ItemTemplate="{StaticResource DataList}"
>          SelectionMode="Multiple"
>          Name="DataListBox" /&gt;


And the Button looks like this:


> &lt;Button Content="Process items"
>         csla:InvokeMethod.TriggerEvent="Click"
>         csla:InvokeMethod.MethodName="ProcessItems"
>         csla:InvokeMethod.MethodParameter="{Binding ElementName=DataListBox, Path=SelectedItems}"/&gt;


And the ViewModel method looks like this:


> public void ProcessItems(System.Collections.ObjectModel.ObservableCollection&lt;object&gt; methodParameter)
> {
>   // process methodParameter
> }


This only works because InvokeMethod refreshes the binding of its MethodParameter property when it gets the Click event from the Button. If it just took the normal binding value, it would always return an empty collection…

But the fact is that InvokeMethod does make this work in a very smooth and easy manner, allowing the ViewModel to implement a method that accepts the list of selected items as a parameter.

#### Multi-select with event trigger

Using the trigger action approach things are really messy, because there’s no way to force a refresh of anything that is bound to SelectedItems.

Worse, you can’t actually bind SelectedItems on the ListBox itself like you bind SelectedItem. In other words, the ListBox ends up looking like this:


> &lt;ListBox ItemsSource="{Binding Path=Model}"
>          ItemTemplate="{StaticResource DataList}"
>          SelectionMode="Multiple"
>          Name="DataListBox"&gt;
> &lt;/ListBox&gt;


Where you’d want to bind SelectedItems to a property of the ViewModel, that’s not possible.

So I thought I’d use a bit of a hack and bind it to the Tag property of the Button:


> &lt;Button Content="Process items"
>         Tag="{Binding ElementName=DataListBox, Path=SelectedItems}"&gt;
>   &lt;i:Interaction.Triggers&gt;
>     &lt;i:EventTrigger EventName="Click"&gt;
>       &lt;csla:Execute MethodName="ProcessItems2" /&gt;
>     &lt;/i:EventTrigger&gt;
>   &lt;/i:Interaction.Triggers&gt;
> &lt;/Button&gt;


While this “works”, it doesn’t really. The problem is that the binding is established when SelectedItems is an empty collection, and it never changes. So this is NOT a useful way to get the list of selected items.

In the end, the solution appears to be that the ViewModel must know that it is dealing with a ListBox so it can get the items directly in the command method. That means the Button must provide a link to the ListBox (via Tag):


> &lt;Button Content="Process items"
>         **Tag="{Binding ElementName=DataListBox}"**&gt;


This way the command method can interact with the Tag property to get a reference to the ListBox to get at the SelectedItems collection:


> public void ProcessItems2(object sender, Csla.Silverlight.ExecuteEventArgs e)
> {
>   var listBox = ((System.Windows.Controls.Control)e.TriggerSource).Tag as System.Windows.Controls.ListBox;
>   var selection = listBox.SelectedItems;
>   // process selection
> }


This is bad because now the ViewModel must know details about the control in the View. It is directly using the ListBox type, which means that the XAML can’t be easily changed to use some other type of list-oriented UI control – at least not without coming back here and changing this code.

I guess one solution would be to create a custom Button subclass that refreshes the binding of its Tag property when the button is clicked – but that’s not a good general solution by any means…

So in the multi-select scenario InvokeMethod is a decent solution, but trigger actions really fall down and the solution seems very inadequate. I think this is primarily due to the implementation of ListBox.SelectedItems, but I also think it is safe to assume that other UI controls will have similarly ill-behaved properties that make trigger actions harder to use than they should be.
