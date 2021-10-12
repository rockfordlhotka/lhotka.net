---
title: VS 2017 and netstandard projects
postDate: 2017-03-30T17:39:30-05:00
abstract: 
postStatus: publish
---
30 March 2017

I really like the new VS 2017 tooling.

However, it has some real problems – it is far from stable for netstandard.

I have a netstandard class library project. Here are issues I’m facing.

1. Every time I edit the compiler directives in the Build tab in project properties it adds YET ANOTHER set of compiler constants for `RELEASE;NETSTANDARD1_6` – those duplicates add up fast!
2. The output path acts really odd – always insists on appending something like `\netstandard1.5\` to the end of the output path – even if the output path already ends with `\netstandard1.5\` - in NO case can I get it to use the path I actually want!! This should act like normal projects imo – not arbitrarily appending crap to my path!
3. I have one netstandard class library referencing another via a *project reference* and this doesn’t seem to be working at all – none of my types from the first class library project seem available in the second
4. The Add References dialog doesn’t show existing references to Shared Projects – the only way to know that the reference is already there is to look at the csproj file in a text editor


We’re going in (what I think) is a good direction with the tooling, but right now it is hard/impossible to integrate netstandard projects into a normal workflow because the tooling is pretty buggy.
