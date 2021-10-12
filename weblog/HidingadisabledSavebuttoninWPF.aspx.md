---
title: Hiding a disabled Save button in WPF
postDate: 2007-09-21T08:01:20.114-05:00
abstract: 
postStatus: publish
---
21 September 2007

I just got back from [VS Live NY](http://www.vslive.com) - which was a great show. It sold out, and the people attending were very engaged and fun to be with. I love crowds like that!

In my all-day workshop on building distributed apps using objects I showed how to use WPF *commanding* to automatically enable/disable Save and Cancel buttons on a form by connecting them to a CslaDataProvider control. That's a really cool feature of WPF that I am leveraging with some of the new [CSLA .NET](http://www.lhotka.net/cslanet) 3.0 features.

An attendee asked if it was possible to *hide* the Save button, not just disable it. I hadn't thought about that, and came up with some answer involving code.

Josh Smith, who was also in the audience, has given this even further thought and sent me an email with a better, pure XAML, solution. Thank you Josh!! Here's the relevant bit of the email:


> During the presentation a fellow asked you how, in WPF, to hide a Button when it is disabled.  The Button was disabled because its associated command could not execute, and he wanted to hide the Button instead of letting it sit in the UI disabled.
>
> The solution you gave him involved some code, which threw a red flag in my mind.  IMO, this is the kind of thing you should use XAML to express, so that there are less "moving parts" in your app.  Here's one way to implement that functionality with no code at all:
>
> &lt;Button Command="Open" Content="\_Open"&gt;
>   &lt;Button.Style&gt;
>     &lt;Style TargetType="Button"&gt;
>       &lt;Style.Triggers&gt;
>         &lt;Trigger Property="IsEnabled" Value="False"&gt;
>           &lt;Setter Property="Visibility" Value="Collapsed" /&gt;
>         &lt;/Trigger&gt;
>       &lt;/Style.Triggers&gt;
>     &lt;/Style&gt;
>   &lt;/Button.Style&gt;
> &lt;/Button&gt;
>
> Depending on your layout, you might want to set Visibility to Hidden instead.

