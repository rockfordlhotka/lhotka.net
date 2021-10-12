---
title: Silverlight 4 RC RichTextBox changes
postDate: 2010-03-18T20:25:40.7515424-05:00
abstract: 
postStatus: publish
---
18 March 2010

I have an app that uses the SL4 RichTextBox control. It is a nice control, and I’ve been enjoying using it. I even went so far as to convert thousands of rows of HTML to Xaml in my database for use with the RTB.

But the control has a couple changes in the new release candidate that I’m having to work around – and if they are not bugs then I’ll have to write a little app to clean the data in my database.

Prior to the RC the minimum value you could set to the Xaml property was “&lt;Section /&gt;”. This was (and is) a pain, because it won’t accept null or string.Empty – so if your actual value is null you need to detect that and change it before trying to set the Xaml property.

But in the RC the minimum value is now “&lt;Section xmlns=\"[http://schemas.microsoft.com/winfx/2006/xaml/presentation\"/](http://schemas.microsoft.com/winfx/2006/xaml/presentation\&quot;/)&gt;”. Not a huge change, but it broke my app of course.

The bigger issue is that prior to the RC the RTB allowed the TextDecorations attribute on the &lt;Section&gt; element. And in fact it *generated this attribute* when it created Xaml.

In the RC the TextDecorations attribute is no longer valid. It isn’t generated, but more importantly it isn’t allowed, so all my Xaml data is invalid.

This is a bit of code that fixes both issues:


> string xaml;
> if (e.NewValue == null)
>   xaml = string.Empty;
> else
>   xaml = e.NewValue.ToString();
> // RTB won't accept an empty string, so if the value is empty/null
> // replace it with the minumum necessary Xaml
> if (string.IsNullOrWhiteSpace(xaml))
>   xaml = "&lt;Section xmlns=\"[http://schemas.microsoft.com/winfx/2006/xaml/presentation\"/](http://schemas.microsoft.com/winfx/2006/xaml/presentation\&quot;/)&gt;";
> // RTB used to support TextDecorations, but now doesn't, so that value
> // must be removed to avoid a crash
> var pos = xaml.IndexOf(" TextDecorations=");
> if (pos &gt;= 0)
> {
>   var closeQuote = xaml.IndexOf("\"", pos);
>   closeQuote = xaml.IndexOf("\"", closeQuote + 1);
>   xaml = xaml.Remove(pos, closeQuote - pos + 1);
> }
> return xaml;


In this case e.NewValue is the Xaml text I’m hoping to put into the control, and the xaml field ends up holding the corrected result.

I’m sure other people moving from the beta to the RC will encounter this same issue. I’m rather hopeful that the TextDecorations thing is a bug so I don’t have to fix all my data, but I suspect it is an intentional breaking change…
