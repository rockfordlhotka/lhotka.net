---
title: CSLA 4 version 4.0.1 released
postDate: 2010-08-28T10:53:42.5441151-05:00
abstract: 
postStatus: publish
---
28 August 2010

CSLA 4 version 4.0.1 is released and available for download.

[Download CSLA 4](http://www.lhotka.net/cslanet/download.aspx)

This is a bug fix release, with [important fixes](http://www.lhotka.net/Article.aspx?id=ef41332f-16a2-441e-81d3-260403a196bf) for some issues in version 4.0.0. If you are using CSLA 4, you should consider upgrading to 4.0.1 as soon as possible.

Please note that there are a couple potential breaking changes in 4.0.1:

- If you are using private backing fields, your RegisterProperty() calls must now specify Relationships.PrivateField so CSLA knows you are using a private backing field. If you don't do this, you'll get runtime exceptions.
- The Save() and BeginSave() methods now raise different (and more reliable) exceptions. If you are explicitly checking for NotSupportedException you will need to check for InvalidOperationException.


While I try to avoid adding breaking changes in point releases, these were important and I thought it better to get them out as early in the CSLA 4 life-cycle as possible.
