---
title: String formatting fun
postDate: 2007-03-13T22:30:21.9815232-05:00
abstract: 
postStatus: publish
---
13 March 2007

String formatting in .NET is a pain. Not that it has ever been easy - even COBOL formatting masks can get out of hand, but there's no doubt that the .NET system is harder to grasp and remember than the VB 1-6 scheme...

I just had a need to format an arbitrary value using a user-supplied format string. You'd think that

obj.ToString(format)

would do the trick. Except that System.Object doesn't have that override of ToString(), so that's not a universal solution. So String.Format() is the obvious next choice, except that I need to somehow take a format string like 'N' or 'd' and make it into something valid for String.Format()...

Brad Abrams has [some good info](http://blogs.msdn.com/brada/archive/2004/01/14/58851.aspx). But his problem/solution isn't quite what I needed. Close enough to extrapolate though:
<font size="2"><p>outValue = </p></font><font color="#0000ff" size="2">string</font><font size="2">.Format(</font><font color="#0000ff" size="2">string</font><font size="2">.Format(</font><font color="#a31515" size="2">"{{0:{0}}}"</font><font size="2">, format), value);</font>
Given a format string of 'N', the inner Format() returns "{0:N}", which is then used by the outer Format() to format the actual value.
