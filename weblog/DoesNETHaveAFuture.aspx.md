---
title: Does .NET Have A Future?
postDate: 2013-10-07T22:24:20.5971842-05:00
abstract: 
postStatus: publish
---
07 October 2013

The short answer to the question of whether the Microsoft .NET Framework (and its related tools and technologies) has a future is *of course, don’t be silly*.

The reality is that successful technologies take years, usually decades, perhaps longer, to fade away. Most people would be shocked at how much of the world runs on RPG, COBOL, FORTRAN, C, and C++ – all languages that became obsolete decades ago. Software written in these languages runs on mainframes and minicomputers (also obsolete decades ago) as well as more modern hardware in some cases. Of course in reality mainframes and minicomputers are still manufactured, so perhaps they aren’t technically “obsolete” except in our minds.

It is reasonable to assume that .NET (and Java) along with their primary platforms (Windows and Unix/Linux) will follow those older languages into the misty twilight of time. And that such a thing will take years, most likely decades, perhaps longer, to occur.

I think it is critical to understand that point, because if you’ve built and bet your career on .NET or Java it is good to know that nothing is really *forcing* you to give them up. Although your chosen technology is already losing (or has lost) its trendiness, and will eventually become extremely obscure, it is a pretty safe bet that you’ll always have work. Even better, odds are good that your skills will become sharply more valuable over time as knowledgeable .NET/Java resources become more rare.

Alternately you may choose some trendier alternative; the only seemingly viable candidate being JavaScript or its spawn such as [CoffeeScript](http://coffeescript.org/) or [TypeScript](http://www.typescriptlang.org/).

How will this fading of .NET/Java technology relevance occur?

To answer I’ll subdivide the software world into two parts: client devices and servers.

### Client Devices

On client devices (PCs, laptops, ultrabooks, tablets, phones, etc.) I feel the need to further split into two parts: consumer apps and business apps. Yes, I know that people seem to think there’s no difference, but as I’ve said before, I think there’s an [important economic distinction between the consumer and business apps](http://www.lhotka.net/weblog/ConsumerVsBusinessApps.aspx).

#### Consumer Apps

Consumer apps are driven by a set of economic factors that make it well worth the investment to build native apps for every platform. In this environment Objective C, Java, and .NET (along with C++) all have a bright future.

*Perhaps* JavaScript will become a contender here, but that presupposes Apple, Google, and Microsoft work to make that possible by undermining their existing proprietary development tooling. There are some strong economic reasons why none of them would want every app on the planet to run equally on every vendor’s device, so this seems unlikely. That said, for reasons I can’t fathom, Microsoft is doing their best to make sure JavaScript really does work well on Windows 8, so perhaps Apple will follow suit and encourage their developers to abandon Objective C in favor of cross-platform JavaScript?

Google already loves the idea of JavaScript and would clearly prefer if we all just wrote every app in JavaScript for Chrome on Android, iOS, and Windows. The only question in my mind is how they will work advertising into all of our Chrome apps in the future?

My interest doesn’t really lie in the consumer app space, as I think relatively few people are going to get rich building casual games, fart apps, metro transit mapping apps, and so forth. From a commercial perspective there is some money to be made building apps for corporations, such as banking apps, brochure-ware apps, travel apps, etc. But even that is a niche market compared to the business app space.

#### Business Apps

Business apps (apps for use by a business’s employees) are driven by an important economic factor called a natural monopoly. Businesses want software that is built and maintained as cheaply as possible. Rewriting the same app several times to get a “native experience” on numerous operating systems has never been viable, and I can’t see where IT budgets will be expanding to enable such waste in the near future. In other words, businesses are almost certain to continue to build business apps in a single language for a single client platform. For a couple decades this has been Windows, with only a small number of language/tool combinations considered viable (VB, PowerBuilder, .NET).

But today businesses are confronted with pressure to write apps that work on the iPad as well as Windows (and outside the US on Android). The only two options available are to write the app 3+ times or to find some cross-platform technology, such as JavaScript.

The natural monopoly concept creates some tension here.

A business might insist on supporting just one platform, probably Windows. A couple years ago I thought Microsoft’s Windows 8 strategy was to make it realistic for businesses to choose Windows and .NET as this single platform. Sadly they’ve created a [side loading cost model](http://www.lhotka.net/weblog/Windows8WinRTLicensingIdeas.aspx) that basically blocks WinRT business app deployment, making Windows far less interesting in terms of being the single platform. The only thing Windows has going for it is Microsoft’s legacy monopoly, which *will* carry them for years, but (barring business-friendly changes to WinRT licensing) is doomed to erode.


> You can probably tell I think Microsoft has royally screwed themselves over with their current Windows 8 business app “strategy”. I’ve been one of the loudest and most consistent voices on this issue for the past couple years, but Microsoft appears oblivious to the problem and has shown no signs of even recognizing the problem much less looking at solutions. I’ve come to the conclusion that they *expect* .NET on the client to fade away, and for Windows to compete as just one of several platforms that can run JavaScript apps. In other words I’ve come to the conclusion that Microsoft is *willingly giving up* on any sort of technology lock-in or differentiation of the Windows client in terms of business app development. They *want* us to write cross-platform JavaScript apps, and they simply hope that businesses and end users will choose Windows for other reasons than because the apps only run on Windows.


Perhaps a business would settle on iOS or Android as the “one client platform”, but that poses serious challenges given that virtually all businesses have massive legacies of Windows apps. The only realistic way to switch clients to iOS or Android is to run all those Windows apps on Citrix servers (or equivalent), and to ensure that the client devices have keyboards and mice so users can actually interact with the legacy Windows apps for the next several years/decades. Android probably has a leg up here because most Android devices have USB ports for keyboards/mice, but really neither iOS nor Android have the peripheral or multi-monitor support necessary to truly replace legacy Windows (Win32/.NET).

This leaves us with the idea that businesses *won’t* choose one platform in the traditional sense, but rather will choose a more abstract runtime: namely JavaScript running in a browser DOM (real or simulated). Today this is pretty hard because of differences between browsers and between browsers on different platforms. JavaScript libraries such as jquery, angular, and many others seek to abstract away those differences, but there’s no doubt that building a JavaScript client app costs more today than building the same app in .NET or some other more mature/consistent technology.

At the same time, only JavaScript really offers any hope of building a client app codebase that can run on iOS, Android, and Windows tablets, ultrabooks. laptops, and PCs. So though it may be more expensive than just writing a .NET app for Windows, JavaScript *might* be cheaper than rewriting the app 3+ times for iOS, Android, and Windows. And there’s always hope that JavaScript (or its offspring like CoffeScript or TypeScript) will rapidly mature enough to make this “platform” more cost-effective.

I look at JavaScript today much like Visual Basic 3 in the early 1990s (or C in the late 1980s). It is typeless and primitive compared to modern C#/VB or Java. To overcome this it relies on tons of external components (VB had its component model, JavaScript has myriad open source libraries). These third party components change rapidly and with little or no cross-coordination, meaning that you are lucky if you have a stable development target for a few weeks (as opposed to .NET or Java where you could have a stable target for months or years). As a result a lot of the development practices we’ve learned and mastered over the past 20 years are no longer relevant, and new practices must be devised, refined, and taught.

Also we must recognize that JavaScript apps *never* go into a pure maintenance mode. Browsers and underlying operating systems, along with the numerous open source libraries you must use, are constantly versioning and changing, so you can never stop updating your app codebase to accommodate this changing landscape. If you do stop, you’ll end up where so many businesses are today: trapped on IE6 and Windows XP because nothing they wrote for IE6 can run on any modern browser. We *know* that is a doomed strategy, so we therefore know that JavaScript apps will require continual rewrites to keep them functional over time.

What I’m getting at here is that businesses have an extremely ugly choice on the client:

1. Rewrite and maintain every app 3+ times to be native on Windows, iOS, and Android
2. Absorb the up-front and ongoing cost of building and maintaining apps in cross-platform JavaScript
3. Select one platform (almost certainly Windows) on which to write all client apps, and require users to use that platform


I *think* I’ve listed those in order from most to least expensive, though numbers 1 and 2 could be reversed in some cases. I think in all cases it is far cheaper for businesses to do what [Delta recently did](http://finance.yahoo.com/news/delta-equip-11-000-pilots-150000465.html) and just issue Windows devices to their employees, thus allowing them to write, maintain, and support apps on a single, predictable platform.

The thing is that businesses are run by humans, and humans are often highly irrational. People are foolishly enamored of BYOD (bring your own device), which might *feel good*, but is ultimately expensive and highly problematic. And executives are often the drivers for alternate platforms because they like their cool new gadgets; oblivious to the reality that supporting their latest tech fad (iPad, Android, whatever) might cost the business many thousands (often easily 100’s of thousands) of dollars each year in software development, maintenance, and support costs.

Of course I work for a software development consulting company. Like all such companies we effectively charge by the hour. So from my perspective I’d really prefer if everyone *did* decide to write all their apps 3+ times, or write them in cross-platform JavaScript. That’s just more work for us, even if objectively it is pretty damn stupid from the perspective of our customers’ software budgets.

### Server Software

Servers are a bit simpler than client devices.

The primary technologies used today on servers are .NET and Java. Though as I pointed out at the start of this post, you shouldn’t discount the amount of COBOL, RPG, FORTRAN, and other legacy languages/tools/platforms that make our world function.

Although JavaScript has a nescient presence on the server via tools like [node.js](http://nodejs.org/), I don’t think any responsible business decision maker is looking at moving away from existing server platform tools in the foreseeable future.

In other words the current 60/40 split (or 50/50, depending on whose numbers you believe) between .NET and Java on the server isn’t likely to change any time soon.

*Personally* I am loath to give up the idea of a common technology platform between client and server – something provided by VB in the 1990s and .NET over the past 13 years. So if we really do end up writing all our client software in JavaScript I’ll be a strong advocate for things like node.js on the server.

In the mid-1990s it was pretty common to write “middle tier” software in C++ and “client tier” software in PowerBuilder or VB. Having observed such projects and the attendant complexity of having a middle tier dev team who theoretically coordinated with the client dev team, I can say that this isn’t a desirable model. I can’t support the idea of a middle tier in .NET and a client tier in JavaScript, because I can’t see how team dynamics and inter-personal communication capabilities have changed enough (or at all) over the past 15 years such that we should expect any better outcome now than we got back then.

So from a server software perspective I think .NET and Java have a perfectly fine future, because the server-side JavaScript concept is even less mature than client-side JavaScript.

At the same time, I really hope that (if we move to JavaScript on the client) JavaScript matures rapidly on both client and server, eliminating the need for .NET/Java on the server as well as the client.

### Conclusion

In the early 1990s I was a VB expert. In fact, I was one of the world’s leading VB champions through the 1990s. So if we are going to select JavaScript as the “one technology to rule them all” I guess I’m OK with going back to something like that world.

I’m not *totally* OK with it, because I rather enjoy modern C#/VB and .NET. And yes, I could easily ride out the rest of my career on .NET, there’s no doubt in my mind. But I have never in my career been a legacy platform developer, and I can’t imagine working in a stagnant and increasingly irrelevant technology, so I doubt I’ll make that choice – stable though it might be.

Fwiw, I do still think Microsoft has a chance to make Windows 8, WinRT, and .NET a viable business app development target into the future. But their time is running out, and as I said earlier they seem oblivious to the danger (or are perhaps embracing the loss of Windows as the primary app dev target on the client). I would *like* to see Microsoft wake up and get a clue, resulting in WinRT and .NET being a viable future for business app dev.

Failing that however, we all need to start putting increasing pressure on vendors (commercial and open source) to mature JavaScript, its related libraries and tools, and its offspring such as TypeScript – on both client and server. The status of JavaScript today is too primitive to replace .NET/Java, and if we’re to go down this road a lot of money and effort needs to be expended rapidly to create a stable, predictable, and productive enterprise-level JavaScript app dev platform.
