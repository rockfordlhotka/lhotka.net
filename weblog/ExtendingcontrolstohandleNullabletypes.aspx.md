---
title: Extending controls to handle Nullable types
postDate: 2006-05-12T08:57:52.359375-05:00
abstract: 
postStatus: publish
---
12 May 2006

I just got back from Norway (so my body has no idea what time it actually is right now...), and one of the conversations I had while there was about data binding a TextBox to an object's property that is a Nullable&lt;T&gt; - like Nullable(Of Integer) or something.

Somehow I had expected that Windows Forms would have anticipated this (obvious) concept and would handle it. Not so...

Fortunately, as a result of this conversation, one of the people at the conference took some of the ideas we were tossing around and [came up with an extender control](http://www.thejoyofcode.com/Databinding_and_Nullable_types_in_WinForms.NET.aspx) to address the issue. Very nice!
