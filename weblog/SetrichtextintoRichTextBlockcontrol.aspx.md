---
title: Set rich text into RichTextBlock control
postDate: 2012-05-11T12:33:13.5976197-05:00
abstract: 
postStatus: publish
---
11 May 2012

Unless I’m missing something, there’s no direct way to bind XAML-ish text to a WinRT RichTextBlock control.

For example, if I have some text like:


> &lt;Paragraph&gt;
>     This is some text. And some &lt;Bold&gt;bolded text&lt;/Bold&gt;.
> &lt;/Paragraph&gt;


I would like to just bind this text to a RichTextBlock control for display. Sadly there’s no way to put content into a RichTextBlock control at runtime short of adding Block objects to the control’s Blocks collection.

As a workaround, I’ve been playing with the idea of a custom control like this:


> using Windows.UI.Xaml;
> using Windows.UI.Xaml.Controls;
> using Windows.UI.Xaml.Markup;
>
> namespace Application11
> {
>   public class RichTextDisplay : ContentControl
>   {
>     public static readonly DependencyProperty XamlProperty =
>         DependencyProperty.Register("Xaml", typeof(string), typeof(RichTextDisplay), new PropertyMetadata(null, XamlChanged));
>
> public string Xaml
>     {
>       get { return (string)GetValue(XamlProperty); }
>       set { SetValue(XamlProperty, value); }
>     }
>
> private static void XamlChanged(object sender, DependencyPropertyChangedEventArgs e)
>     {
>       var ctl = (RichTextDisplay)sender;
>       var xaml = new System.Text.StringBuilder();
>       xaml.Append(@"
> &lt;UserControl
>   xmlns=""[http://schemas.microsoft.com/winfx/2006/xaml/presentation""](http://schemas.microsoft.com/winfx/2006/xaml/presentation&quot;&quot;)
>   xmlns:x=""[http://schemas.microsoft.com/winfx/2006/xaml""](http://schemas.microsoft.com/winfx/2006/xaml&quot;&quot;)
>   xmlns:mc=""[http://schemas.openxmlformats.org/markup-compatibility/2006""](http://schemas.openxmlformats.org/markup-compatibility/2006&quot;&quot;)&gt;
>   &lt;Grid&gt;
>     &lt;RichTextBlock&gt;");
>       xaml.Append(ctl.Xaml);
>       xaml.Append(@"
>     &lt;/RichTextBlock&gt;
>   &lt;/Grid&gt;
> &lt;/UserControl&gt;
> ");
>       var text = xaml.ToString();
>       var xr = (Control)XamlReader.Load(text);
>
> ctl.Content = xr;
>     }
>   }
> }


This isn’t ideal, but it does work. The RichTextDisplay control dynamically creates a RichTextBlock control, inserting the XAML document text into the body of the newly created control.

I suppose the other alternative would be to write code that parses the text to find the XAML elements and produces a series of Block objects that can be added to the control’s Blocks collection…
