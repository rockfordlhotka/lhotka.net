---
title: Windows 8 on a laptop
postDate: 2012-03-07T16:48:41.6629814-06:00
abstract: 
postStatus: publish
---
07 March 2012

I’ve spent a couple days using Windows 8 on my laptop now. And I’ve been using it on my tablet for a long time (Dev Preview and now Consumer Preview).

To get this out of the way right off: Windows 8 is clearly designed for tablets first, and desktop/laptop machines second. I really enjoy using it on the tablet, and it is fine on the laptop, but perhaps not as nice as Windows 7.

### Performance

It is (or feels) faster than Win7 on the same machine. Win8 is just snappy. Microsoft likes the phrase “fast and fluid”, and it is fluid with touch, but it is snappy with keyboard/mouse.

### Desktop usage

I’ve now pinned my common apps to the desktop start bar, just like I did with Win7. I had all my apps pinned in Win7 too, and rarely used the Start menu to launch anything, and the same is true in Win8.

I am finding that I rarely leave the desktop at all really. So in that regard, Win8 is just a slightly faster Win7. Most of what I’ve been doing has involved the use of Outlook, Word, Excel, IE, and Visual Studio – all of which run happily on the desktop, and so I often forget that I’m running Win8.

### WinRT Metro style usage

When I do leave the desktop for WinRT, it has been to launch apps so I can pin them on the desktop start bar, or to play around with the various Metro style apps available. I’ve already discussed how pinning the apps on the desktop leads to a Win7-like experience, so I’ll now move on to my thoughts on using the Metro style apps with keyboard/mouse.

By way of disclaimer, I find the various Metro style apps to be incredibly inconsistent on both the tablet and laptop. They are clearly all works in progress. Some are better than others, but the lack of consistency in terms of the “back” concept and general navigation is really annoying. Microsoft has a lot of work to do just to get their own Metro style apps to be consistent and pleasant, and I don’t know how they will convince the creators of other apps to do a better job…

(as an aside, iPad users have told me that they are often frustrated with the lack of consistency across iPad apps too – so maybe this is just the future we’re embracing – one where every app makes up its own rules and us users have to just suck it up…)

### “Back” concept frustration

<sub></sub><sub></sub>My biggest issue with Metro style apps is the “back” concept. This comes in two forms: there are two “back” concepts, and apps don’t consistently implement the “back” concept they control.

First, a left-swipe is “back” to the previous app, and this is an OS concept. And apps can implement their own “back” concept, often with an arrow pointing left, or an X icon, or something else – and that moves you back *within the context of the app*.

Having these two back concepts isn’t so bad until one app launches another. The most common scenario is the People hub launching IE. So I was in the People hub, reading what people have been doing, now I’m in IE. I might click on a couple links in IE too. So now I can use the IE back button to move back through IE, but I (the human user) have to know to use a left-swipe to get back to the People hub. Personally I find this jarring and frustrating. Especially when compared to Windows Phone, where the back button would take me back through the web pages, and then back to the People hub. Smooth and consistent.

(I suspect it is too late in the game for Microsoft to address this issue – but I also suspect it will be the butt of jokes about Win8 UX design for the next decade or so, because it is a serious PITA)

To make this whole thing worse, the “back” concept implemented by each app is really under the app’s control. And every app seems to make up their own way to handle the scenario. Some examples:

- The back button is always visible in the upper-left of the UI, wasting space, and not near my thumb (on the tablet) so I have to shift my hands to go back – yuck!
- The back button is in the app bar, but in the top bar, not the bottom, forcing me to swipe or right-click in the app bar, then shift my hands to go back – super yuck!
- The back button is in the upper-right corner (either ways visible or in the app bar) – which is amazingly terrible!
- The back button is in the app bar in the lower-left, forcing me to swipe or right-click in the app bar, but at least I don’t have to shift my hands – this is so so…


On a laptop, I’m constantly moving my mouse this way and that to find and click the back/close buttons where ever a particular app decided to put the button.

Personally, I think Microsoft should have put a Back button on the actual device like they did on the phone. Or the left-swipe should be back for the app, and then the OS, more like the WP7 back button… Again, I suspect we’re just in for a lot of pain and jokes for years to come ![Sad smile](binary/Windows-Live-Writer/Windows-8-on-a-laptop_E309/wlEmoticon-sadsmile_2.png)

### Mouse support

The start screen and most Metro style apps provide some basic support for the mouse. Nothing spectacular, but there are scrollbars for panning and scrolling and they work fine. Right-click is like swiping in the app bar with touch.

Some things are still easier with the mouse, like selecting something and interacting with it. Much more precise and reliable with the mouse than with touch.

On the whole, the mouse support in Metro style apps is adequate, but not particularly good. That’s true for the start screen and all the other apps I tried.

**Update:** After installing the touchpad driver and enabling the various scroll/pan/zoom/rotate gestures supported by the touchpad, I am finding the “mouse” experience to be much more satisfying in Metro style apps. I’m not sure if this really counts, because these aren’t technically “mouse” gestures. But for a laptop user with a decent touchpad (like on my Dell), this does make a big difference.

### Keyboard “support”

The start screen has a bunch of Windows key shortcuts for the keyboard. Learn these and the start screen becomes quite pleasant (imo) for a keyboard/mouse user. The start screen’s mouse support is limited, but with the keyboard shortcuts it is easy to be fast and productive from the start screen.

Individual apps do or don’t work with the keyboard much or at all. Few of the apps seem to take the keyboard into account much at all, and others use the keyboard, but not in a way I find intuitive.

For example, the US News app (which is visually stunning) uses left and right arrow keys to move between news stories. But there doesn’t seem to be any way to use the keyboard to pan the current story left or right. Because all stories must be panned left to read the text, the result is that you *must* use the mouse and scrollbar to read the story. That’s just lame.

I’d have expected left/right arrows to pan the story, and perhaps page-up/down to move between stories.

Other apps do use left/right arrow to pan the current item, but usually at such a slow rate of panning as to be useless.

I know, these apps were rushed out so they could be in the store for the Consumer Preview launch. And I’m sure the primary focus was on touch, not keyboard/mouse support.

On the other hand, I’m hoping that by recording my thoughts and experiences as a laptop user, future versions of these apps, and other future apps, will remember that desktop/laptop users will run Win8 too, and that these apps need to support non-touch devices as well as touch.

### Metro style summary

Microsoft has made it clear that their *intent* is for Metro style apps to treat touch as a first-class interaction model. Other than the apps having the consistency of the web in 1997 (which is to say none), I would say that they’ve achieved that goal. These apps are all about touch.

But Microsoft also made it clear that their intent is for keyboard/mouse to be a first-class interaction model. The start screen certainly treats the keyboard as first-class. The mouse is probably second-class at this point. Individual Metro style apps are pretty much completely treating keyboard/mouse as an afterthought – let’s go with third-class.

So this is a call to Microsoft to stick with their intent and to keep pushing the keyboard/mouse and touch models *in parallel* and *with parity*.

And even more, this is a reminder to all of us app developers that *it is our responsibility* to ensure that keyboard/mouse and touch users are all happy with our user experience designs.

Finally, it is a call to Microsoft to do *something* about the horrible “back” concept issue. Again, I recognize it is probably too late to fix the dual model issue. But at least provide some STRONG guidance (and a consistent example in your own apps) on how to implement the application back concept. For lack of anything better, my vote is for an always-visible button in the lower-left of the screen. Don’t make me bring up the app bar, and *really* don’t make me shift my hands to reach the top (left or right) of the screen.

### Close

To close, I am finding Win8 to be a perfectly good beta experience. Is it ready for prime time? Of course not, it is a beta. If you install it on a machine can you be productive and happy? Absolutely yes.

This is especially true if you (like me) are already used to pinning your common apps to the desktop start bar. Do that, and you’ll hardly know you are running Win8 at all.

The immature state of the Metro style apps doesn’t really worry me. As more and more people use these apps and provide feedback like I’m doing here, the user experiences provided by those (and future) apps will improve for touch and keyboard/mouse users alike.

I’m quite excited about Win8 and WinRT and the future of the platform. It really does bring user experience into the forefront of application development. The difference between apps that have attention to UX and those that don’t is the difference between a usable app and one that sucks productivity and joy from life.

It is now up to all of us as developers to recognize this reality, and to provide a UX that does bring joy and productivity to our users – keyboard, mouse, or touch.
