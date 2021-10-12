---
title: Windows Forms data binding issue in VS 2005
postDate: 2005-09-23T18:46:01.46875-05:00
abstract: Problematic issue when using data binding against smart data containers
postStatus: publish
---
23 September 2005

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I recently discovered an issue with Windows Forms data binding when a form is bound against a smart data container like a DataTable with partial class code or a CSLA .NET –style object. The issue is pretty subtle, but nasty – and my current workaround doesn’t thrill me. So after reading this if you have a better work around I’m all ears – otherwise this could end up in the books I’m current writing, since both are impacted… :(</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So here’s the problem:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Create a smart data source – defined as one that includes business logic such as validation and manipulation of data. In this case, it is the manipulation part that’s the issue. For instance, maybe you have a business rule that a given text field must always be upper case, and so you properly implement this behavior in your business object or partial class of your DataTable to keep that business logic out of the UI.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In a business object for instance, this code would be in the property set block – perhaps something like this in a CSLA .NET 2.0 style class:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> LastName() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>VerifyGetProperty(</font>"LastName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mLastName<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>VerifySetProperty(</font>"LastName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>If<font color="#000000"> mLastName &lt;&gt; value </font>Then<o:p></o:p>

**<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mLastName = value.ToUpper<o:p></o:p></font>**

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged(</font>"LastName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>If<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">(in CSLA .NET 2.0 the PropertyHasChanged method raises the appropriate PropertyChanged event via the INotifyPropertyChanged interface and also calls MarkDirty)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Or a simpler class that implements INotifyPropertyChanged:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> LastName() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mLastName<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

**<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mLastName = value.ToUpper<o:p></o:p></font>**

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>RaiseEvent<font color="#000000"> PropertyChanged(</font>Me<font color="#000000">, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>New<font color="#000000"> PropertyChangedEventArgs("LastName"))<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Specifically notice that the inbound value is changed to upper case with a ToUpper call in the set block.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now add that data container to the Data Sources window and drag it onto your form in Details mode. Visual Studio nicely creates a set of controls reflecting your properties/columns (damn I love this feature!!) and sets up all the data binding for you. So far so good.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now run the application and enter a lower case value into the Last Name text box and tab off that control. Data binding automatically puts the new value into the object and runs the code in the set block. This means the object now contains an upper case version of the value you entered.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Notice that the TextBox control <i style="mso-bidi-font-style: normal">does not</i> reflect the upper case value. The value from the object was never refreshed in the control.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now change another value in a different control and tab out. Notice that the Last Name TextBox control is <i style="mso-bidi-font-style: normal">now</i> updated with the upper case value.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So that’s the problem. Data binding updates all controls on a form when a PropertyChanged event is raised, <i style="mso-bidi-font-style: normal">except the current control</i>. You can put a breakpoint in the property get block and you’ll see that the value isn’t retrieved until some other control triggers the data binding refresh.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>
<font face="Times New Roman" color="#000000" size="3"><p class="MsoNormal" style="MARGIN: 0in 0in 0pt"><o:p><font face="Times New Roman" color="#000000" size="3">I did <a href="http://lab.msdn.microsoft.com/productfeedback/viewfeedback.aspx?feedbackid=89c42d15-dfb0-433f-ac41-12470c02f99f">report this bug to Microsoft</a>, but it has been marked as postponed - meaning that it won't get fixed for release. An unfortunate side-issue is that this issue makes data binding in 2.0 work differently than in .NET 1.x, so any .NET 1.x code that binds against a smart data container like a business object will likely quit working right under 2.0.</font></o:p></p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt"><o:p><font face="Times New Roman" color="#000000" size="3"></font></o:p>&nbsp;</p>
<p class="MsoNormal" style="MARGIN: 0in 0in 0pt">Now to my workaround (of which I’m not overly proud, but which does work). My friend Ed Ferron should get a serious kick out of this – feel free to laugh all you’d like Ed!</p></font>
<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The problem is that data binding isn’t refreshing whatever control is currently being edited when the PropertyChanged event is raised. The obvious question then is how to get a PropertyChanged event raised <i style="mso-bidi-font-style: normal">after</i> the property set block has completed. Because at that point data binding will actually refresh the control.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The easiest way to get some action to occur “asynchronously” without actually using multi-threading (which would be serious overkill) is to use the System.Windows.Forms.Timer control. That control runs on your current thread, but provides a simulation of asynchronous behavior. (On the VAX this was called an asynchronous trap, so the concept has been around for a while!)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Putting the Timer control into your data object is problematic. The Timer control implements IDisposable, so your object would also need to implement IDisposable – and then any objects using your object would need to implement IDisposable. It gets seriously messy.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Additionally, a real application may have dozens or hundreds of objects. They can’t each have a timer – that’d be nuts! And the OS would run out of resources of course.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But there’s a solution. Use a shared Timer control in a central location. Like this one:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

Public<font color="#000000"> </font>Class<font color="#000000"> Notifier<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">#</font>Region<font color="#000000"> </font>" Request class "<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Class<font color="#000000"> Request<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Public<font color="#000000"> Method </font>As<font color="#000000"> Notify<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Public<font color="#000000"> PropertyName </font>As<font color="#000000"> </font>String<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Public<font color="#000000"> </font>Sub<font color="#000000"> </font>New<font color="#000000">(</font>ByVal<font color="#000000"> method </font>As<font color="#000000"> Notify, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>ByVal<font color="#000000"> propertyName </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Me<font color="#000000">.Method = method<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Me<font color="#000000">.PropertyName = propertyName<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Class<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">#</font>End<font color="#000000"> </font>Region<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Delegate<font color="#000000"> </font>Sub<font color="#000000"> Notify(</font>ByVal<font color="#000000"> state </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Shared<font color="#000000"> mObjects </font>As<font color="#000000"> </font>New<font color="#000000"> Queue(</font>Of<font color="#000000"> Request)<o:p></o:p></font>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Shared<font color="#000000"> </font>WithEvents<font color="#000000"> mTimer </font>As<font color="#000000"> </font>New<font color="#000000"> System.Windows.Forms.Timer<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Shared<font color="#000000"> </font>Sub<font color="#000000"> RequestNotification(</font>ByVal<font color="#000000"> method </font>As<font color="#000000"> Notify, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>ByVal<font color="#000000"> propertyName </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mObjects.Enqueue(</font>New<font color="#000000"> Request(method, propertyName))<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mTimer.Enabled = </font>True<o:p></o:p>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Shared<font color="#000000"> </font>Sub<font color="#000000"> </font>New<font color="#000000">()<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mTimer.Enabled = </font>False<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mTimer.Interval = 1<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

<font color="#000000">&nbsp; </font>Private<font color="#000000"> </font>Shared<font color="#000000"> </font>Sub<font color="#000000"> mTimer_Tick(</font>ByVal<font color="#000000"> sender </font>As<font color="#000000"> </font>Object<font color="#000000">, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>ByVal<font color="#000000"> e </font>As<font color="#000000"> System.EventArgs) </font>Handles<font color="#000000"> mTimer.Tick<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>mTimer.Enabled = </font>False<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>While<font color="#000000"> mObjects.Count &gt; 0<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Dim<font color="#000000"> request </font>As<font color="#000000"> Request = mObjects.Dequeue<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>request.Method.Invoke(request.PropertyName)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>While<o:p></o:p>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p>&nbsp;</o:p>

End<font color="#000000"> </font>Class<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This could alternately be implemented as a singleton object, but the usage syntax for this is quite nice. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This Notifier class really implements the RequestNotification method, allowing an object to request that the Notifier call the object back in 1 tick of the clock (about 100 nanoseconds) on a specific method.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The reason the class maintains a list of objects to notify is because even in a single threaded application you can easily envision a scenario where multiple notification requests are registered within 100 nanoseconds – all you need is programmatic loading of data into an object.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now your data object must implement a method matching the Notify delegate and register for the callback. For instance, here’s the updated code from above:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Property<font color="#000000"> LastName() </font>As<font color="#000000"> </font>String<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Return<font color="#000000"> mLastName<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Get<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>Set<font color="#000000">(</font>ByVal<font color="#000000"> value </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mLastName = value.ToUpper<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Notifier.RequestNotification(</font>AddressOf<font color="#000000"> Notify, </font>"LastName"<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>End<font color="#000000"> </font>Set<o:p></o:p>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Property<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">&nbsp; </font>Public<font color="#000000"> </font>Sub<font color="#000000"> Notify(</font>ByVal<font color="#000000"> propertyName </font>As<font color="#000000"> </font>String<font color="#000000">)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>RaiseEvent<font color="#000000"> PropertyChanged(</font>Me<font color="#000000">, _<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp; </font>New<font color="#000000"> PropertyChangedEventArgs(propertyName))<o:p></o:p></font>

<font color="#000000">&nbsp; </font>End<font color="#000000"> </font>Sub<o:p></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Rather than raising the event directly, the property set block now asks the Notifier to call the Notify method in 1 tick. So 1 tick later – after the property set block is complete and data binding has moved on – the Notify method is called and the appropriate PropertyChanged event is raised.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">With this change (hack) data binding will now refresh the Last Name TextBox control as you tab out of it. Though there’s a 100 nanosecond delay in there, it isn’t something the user can actually see and so you can argue it doesn’t matter.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I can hear Ed laughing already…</font>
