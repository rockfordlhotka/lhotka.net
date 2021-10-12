---
title: Getting CSLA 4 to compile for WP7
postDate: 2010-07-29T21:19:10.4576424-05:00
abstract: 
postStatus: publish
---
29 July 2010

This is kind of a running commentary, or personal log (stardate July 2010), recording the various things I had to do to get the CSLA 4 Silverlight codebase to build in the WP7 (Windows Phone 7) beta SDK.

This has nothing to do with getting anything actually running – this is just the stuff I had to change to get the code to compile.

To create the Csla.Wp project, I just linked in files from Csla and Csla.Silverlight. There are almost no actual files in Csla.Wp – it is almost completely reusing the same code used to implement Csla.Silverlight. That’s really cool, as it means my maintenance burden is (theoretically) quite low.

(though this exercise did highlight the need for me to go through the Csla and Csla.Silverlight projects to remove all code files from the Csla.Silverlight project too – ideally there’d be exactly one of any given file, with a few #if statements to deal with platform differences – but that’s a task for another day)

Most of my issues building on WP7 turned out to be caused by the fact that CSLA 4 targets Silverlight 4, and WP7 is based on SL3.

- Missing: DataAnnotations
- Missing: Reflection.Emit
- Missing: Lambda expressions
- Missing: string.IsNullOrWhiteSpace
- Missing: Browsable attribute


Most of the DataAnnotations code I just had to block out with #if statements, though I did create my own DisplayAttribute class because I don’t want to lose that particular feature (the friendly name part). So business classes using that particular attribute should work fine, but the other DataAnnotations attributes won’t compile in WP7.

I also created my own BrowsableAttribute class, even though it doesn’t do anything. This saved me from littering tons and tons of code with #if statements, and I can’t see where it hurts anything to have this dummy attribute in my code. The attribute normally just affects the behavior of Visual Studio, which wouldn’t be affected either way.

The IsNullOrWhiteSpace method I just replaced with the (not as good) IsNullOrEmpty using #if statements. A little cluttered, but a workable answer.

What I’m working on now is the final part: dealing with the lack of lambda expressions and dynamic methods. Basically I need to revert the CSLA code back to using raw reflection in those cases, since none of the modern reflection alternatives appear to exist in WP7. That shouldn’t be too hard, as I can get most of that older code from earlier versions of CSLA and just put it into the existing codebase using #if statements (so I don’t affect the .NET or SL implementations).

Given the size and complexity of CSLA 4, I’m really quite pleased with the relative easy by which I’ve been able to get the code to (almost) build in WP7.
