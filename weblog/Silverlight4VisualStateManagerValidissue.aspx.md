---
title: Silverlight 4 VisualStateManager Valid issue
postDate: 2010-06-29T15:58:25.7793449-05:00
abstract: 
postStatus: publish
---
29 June 2010

CSLA includes a control called PropertyStatus, which is somewhat like the Windows Forms ErrorProvider, but far more powerful. It displays error, warning and informational messages from the business object property to which it is bound, and also exposes various metadata properties so other UI elements can bind in interesting ways (like disabling or hiding parts of the UI if the user isn’t authorized to view or edit a property).

The PropertyStatus control has been around for a couple years, in Silverlight 2 and 3 and WPF 3.5.

It broke in Silverlight 4 (but not WPF 4). I spent most of today trying to figure out why. What changed? We’d made a few changes to the control as part of the CSLA 4 project, but nothing really major – certainly nothing that seemed like it should make the control fail in SL4 and work in WPF (it is the same control for both technologies).

After a couple hours of frustration with the debugger, I enlisted the help of my friend and colleague Justin Chase. We fired up SharedView and spent a couple more hours of quality time with the VS10 debugger.

Nothing made sense. The problem was that the control would just disappear. If it was displaying an error icon, and the property was changed, but remained in error, the icon would disappear – the control would vanish.

The control is written using the VisualStateManager (VSM). So whether it is visible or not depends on which visual state is current. States are Valid, Error, Warning, Information, Busy.

There’s exactly one line of code in the control that calls the VMS GoToState() method. We could watch the code set the visual state to Error. And then we could watch the control vanish from the UI shortly thereafter.

Justin had the bright idea to put non-blank content in the Valid and Busy states (because normally they are empty). That worked – it turned out that *something* was setting the state to Valid.

We searched rather thoroughly through the CSLA codebase trying to find anything that might be using the VSM to set the state to Valid. We commented out most of the code in the control – including the one GoToState() call. We made sure CSLA was not setting the visual state.

And yet the state was being set to Valid.

So we changed the name of the state from Valid to Foo. That fixed the problem. Whatever code (presumably in the Silverlight runtime???) that was setting the state to Valid was no longer impacting us, because we no longer had a Valid state.

I assume this has something to do with the new validation concepts built into Silverlight 4. But talk about nasty! Apparently something in Silverlight runs through the visual tree, setting visual states of controls to “Valid” if that state is defined. I rather suspect there are other “reserved states” as well – but I don’t know for sure.

Of course my theory could be wrong, and perhaps it is yet something else that is setting visual states to Valid – but my money is on the Silverlight 4 validation system…

This is a horrific breaking change from SL3 to SL4, primarily because it isn’t something you’d expect. To have some other code hijack your visual states just because of how they are named – that’s really unpleasant.

So I’m blogging this in the hopes that anyone else using the VSM with a state name of “Valid” can avoid spending as many hours as Justin and I just did trying to figure out the problem…
