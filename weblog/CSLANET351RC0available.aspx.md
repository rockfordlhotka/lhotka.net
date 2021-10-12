---
title: CSLA .NET 3.5.1 RC0 available
postDate: 2008-07-27T17:05:08.285304-05:00
abstract: 
postStatus: publish
---
27 July 2008

I have put CSLA .NET 3.5.1 release candidate 0 online at http://www.lhotka.net/cslanet/download.aspx.

Version 3.5.1 has some *very* important bug fixes for 3.5, especially around some of the new property syntax and Windows Forms data binding.

If you are using any of the new 3.5 property syntax, or are using Windows Forms data binding, you *really* should test 3.5.1 ASAP!

There's only one breaking change in how a "new PropertyInfo(...)" expression is written - I had to remove a constructor. This is unfortunate, but necessary, because the overload was ambiguous with another overload when the property type was string. The compiler will find these for you, and they are easily resolved - just check the change log for info.

Beta 2 was quite stable - no bug reports, only one feature change for data binding - so I expect RC0 to be very good. Please let me know if you encounter issues.
