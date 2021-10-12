---
title: Using the TriggerAction control
postDate: 2011-02-18T17:31:39.3397769-06:00
abstract: 
postStatus: publish
---
18 February 2011

[Bxf](http://bxf.codeplex.com) and CSLA .NET both include a TriggerAction control. This control helps support the MVVM design pattern in WPF, Silverlight, and WP7 applications.

(Bxf is completely independent from CSLA – I donated TriggerAction from CSLA to the Bxf project a while back though, so this type is available from either framework)

The specific problem addressed by TriggerAction is the need to invoke a verb (method/command) on your viewmodel object in response to any arbitrary UI event. One common UI event is something like a button click event, though you can often use commanding in that case. But there are numerous other UI events from many controls other than buttons, and you might want to have one of those UI events cause the viewmodel to perform an action.

TriggerAction basically wires arbitrary UI events to methods on the current DataContext (usually the viewmodel object).


> <font face="Courier New">&lt;bxf:TriggerAction TargetControl=&quot;{Binding ElementName=MyControl}&quot;       <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; TriggerEvent=&quot;MouseOver&quot;        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; DataContext=&quot;{Binding Source={StaticResource vm}}&quot;        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; MethodName=&quot;MyAction&quot; /&gt;</font>


TriggerAction listens for the trigger event from the TargetControl. When it handles that event, it invokes the specified method (MethodName) on its current DataContext object. There’s nothing more to it.

To get TriggerAction working you need two things: source and target.

Source:

1. TargetControl must be set
2. TriggerEvent may be set (default is “Click”)


Target:

1. DataContext must be set (or inherited from the container)
2. MethodName must be set


Parameter (optional):

1. MethodParameter may be set (to a value or binding expression)
2. RebindParameterDynamically may be set to true (to force rebinding of MethodParameter to work around issues with certain control properties such as ListBox.SelectedItems)


The most common causes of failure when using TriggerAction are that the TargetControl isn’t set right, or the DataContext isn’t set right, and of those two the most common is that the DataContext isn’t what you think it is (that happens to me all the time).

The method TriggerAction invokes on the DataContext object can accept either 0 or 2 parameters:


> public void MyAction()


or


> public void MyAction(object sender, ExecuteEventArgs e)


The ExecuteEventArgs class is also defined in Bxf and CSLA. If you use TriggerAction from Bxf.Xaml, you *must* use ExecuteEventArgs from Bxf.Xaml. If you use TriggerAction from Csla.Xaml, you *must* use ExecuteEventArgs from Csla.Xaml.

If you are using Bxf and CSLA together it is important to understand that the ViewModel&lt;T&gt; class from Csla.Xaml uses the Csla.Xaml.ExecuteEventArgs type. If you are using the Bxf TriggerAction control, you’ll need to create your own viewmodel types from Csla.Xaml.ViewModelBase&lt;T&gt; to accept the Bxf.Xaml.ExecuteEventArgs type.
