---
title: MCsla &ndash; compiling DSL source into M
postDate: 2009-04-21T20:54:06.914182-05:00
abstract: 
postStatus: publish
---
21 April 2009

Working with [Microsoft Oslo](http://msdn.com/oslo), the goal is to enable the creation of a domain specific language (DSL) using MGrammar, so a developer can write code in that grammar, compile the code into M and then load that M into the Oslo repository.

This is turning out to be a bigger challenge that you’d expect, though I think that’s largely because I’m dealing with such early builds of all the Oslo tools.

The tool chain for compiling DSL source into M is this:

1. Use mg.exe to compile the MGrammar
2. Use mgx.exe to compile the DSL source against the grammar to create M
3. Use m.exe to compile the M
4. Use mx.exe to load the compiled M (an mx file) into the repository


Unfortunately this breaks down at step 2, because mgx.exe has some issues.

The first issue I encountered was that mgx creates *hierarchical M*, not *relational M*. What’s the difference?

Relational M is defined by an MSchema where child entities define foreign key relationships to their parent. This is the normal model you’d find when creating any relational database.

Hierarchical M is defined by an MSchema where *parent* entities define relationships with their children. This is more like what you’d find in XML, and doesn’t completely map to a normal relational model. While it is true that this type of MSchema can result in valid SQL table definitions, you can’t define all the relationship restrictions you’d normally want to have in your database.

The thing is, M code itself must match the shape of the MSchema you want to use. So if you define your entities using a relational MSchema, the M must also be relational. Conversely, this means that when mgx generations hierarchical M, you *must* use a hierarchical MSchema to map that M metadata into your database (or the Oslo repository).

This is an unfortunate limitation, that hopefully will be resolved at some point.

The second and third issues I encountered appear to be bugs in mgx. But not just in mgx – they are bugs in the underlying API, so even if you try to write your own “mgx replacement” (which is what I’m doing btw), the API that helps you generate M will create invalid M output.

The two bugs are:

1. When a node has a Boolean value, true comes out as ‘ true’ and false comes out as ‘ false’. The single quotes and space after the first single quote should not be there, but that’s what gets output. Oddly enough, Int32 and other primitive types work fine – just Boolean types seem to be broken.
2. When a list of items is output, and that list contains one item, the output is invalid M. Multiple items or no items in the list work fine – just the single-item case is broken.


The only solution I’ve found for these bugs is to do a post-processing step on the resulting M – literally doing text processing to identify and fix the issues. Again, hopefully these issues get resolved in the API itself, so valid M gets produced by mgx or any other tool using the API.

The fourth issue, and the reason I’m writing my own mgx replacement, is that my MCsla grammar allows arbitrary placement of various elements, like authorization and business rules within a property:


> Public string Name {
>   Allow Write (“Admin”, “Supervisor”);
>   Rule StringRequired;
>   Deny Read (“Guest”);
> }


Because the grammar allows arbitrary placement, the resulting M is a collection of mixed types of entity. In other words, the compiled M is effectively invalid, because the M parser can’t figure out whether the collection contains auth rules, or business rules (because it contains both).

I really have two choices – either change my grammar to put auth rules and business rules in different block structures, or at least to require one to come before the other. Or write my own mgx replacement to rearrange the nodes of the compiled DSL code into discrete collections of homogeneous types.

Since I don’t want to “ruin” my pretty grammar, I’m trying to fix the nodes by creating my own mgx replacement. And this seems quite realistic, though it doesn’t address the first three issues in any way – those are still problematic.
