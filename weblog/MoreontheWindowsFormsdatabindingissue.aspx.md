---
title: More on the Windows Forms data binding issue
postDate: 2005-09-25T21:50:02.71875-05:00
abstract: ...following on from discussions in the previous blog entry...
postStatus: publish
---
25 September 2005

<font face="Times New Roman" color="#000000" size="3">In my </font>[<font face="Times New Roman" size="3">last post</font>](http://www.lhotka.net/WeBlog/PermaLink.aspx?guid=37bc1b86-fbdc-45fa-be8a-2fb66f9e2447)<font face="Times New Roman" color="#000000" size="3"> I discussed a nasty bug with Windows Forms data binding, along with one possible solution (which is most certainly a hack). This led to some discussion – including a couple people observing that this hack should probably be in the UI layer, not the business layer (which is where I’d put it).</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In concept I agree with the idea that the hack could belong in the UI layer. However, that is a slippery slope for two reasons. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">First, you could argue that all data binding support only exists for Windows Forms, since neither Web Forms and certainly Web services utilize any of the interfaces or event models required by data binding. Yet it is quite obvious that data binding requires that the data source itself implement these behaviors in order to work properly. The hack is merely overcoming a bug in the way data binding works, so it naturally fits along with all the other interfaces and eventing that already exist in the data source.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Second, it is a hack. One would hope that this is a temporary issue that Microsoft will fix. Remember that this will break all .NET 1.x code that uses data binding where the data source actually manipulates data! It would seem likely that it would be a high priority to fix this issue (we can only hope). Thus it is less important where the hack is placed, than it is how transparent it is and how easily it can be removed in the future when (if) Microsoft fixes this bug.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the case of CSLA .NET 2.0 I can entirely embed the hack into the framework, meaning that removing the hack in the future would be a simple framework change. In the case of custom objects or smart DataTables a well-implemented hack could be removed by changing just a few lines (3-6) of code in each object.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But let’s consider the idea of solving this in the UI. The obvious solution in the UI is to add a LostFocus handler for every control and just updating the control at that point – thus directly overcoming the issue at hand. I’m sure there are various other possibilities, but the problem is merely that the value isn’t updated automatically at LostFocus, so it is hard to imagine a more direct or simple solution than to just update it directly.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">That turns out to be brainless code in every form in the system. It is brainless enough that you could use a little reflection and generically wrap it up into a new base form class so when the form loads it hooks LostFocus for all events, and the event handler loops through all bindings on the control and refreshes any and all values associated with those bindings. This is effectively what data binding does anyway, so we’d be simply replicating what they should be doing for the control.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Wrapping this up into a new base form class is the way to go obviously – since it avoids writing this code in every form. However, it does require the use of reflection and forces all forms to inherit from this new base class – which is a PITA.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I think it would be a bit more invasive to remove the hack from the UI than from CSLA .NET. However, it may be <i style="mso-bidi-font-style: normal">less</i> invasive to remove the hack from the UI than to remove it from custom objects or smart DataTable objects.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So I will likely show the UI hack in the smart DataTable book, and the Timer hack in the Business Objects books (barring some better hacks or a real fix from Microsoft).</font>
