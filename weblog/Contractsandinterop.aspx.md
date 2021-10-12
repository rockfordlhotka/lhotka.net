---
title: Contracts and interop
postDate: 2005-02-23T15:00:15.671875-06:00
abstract: Loose-coupling and contract-based implementation are antithetical
postStatus: publish
---
23 February 2005

Just a super-quick entry that I'll hopefully follow up on later. Ted [wrote a bunch of stuff](http://www.neward.net/ted/weblog/index.jsp?date=20050222#1109140047640) on contracts related to Indigo, etc.



I think this is all wrong-headed. The idea of being loosely coupled and the idea of being bound by a contract are in direct conflict with each other. If your service only accepts messages conforming to a strict contract (XSD, C#, VB or whatever) then it is impossible to be loosely coupled. Clients that can't conform to the contract can't play, and the service can *never ever* change the contract so it becomes locked in time.



Contract-based thinking was all the rage with COM, and look where it got us. Cool things like DoWork(), DoWork2(), DoWorkEx(), DoWorkEx2() and more.



Is this *really* the future of services? You gotta be kidding!
