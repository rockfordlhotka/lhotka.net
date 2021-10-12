---
title: Issues with WPF page navigation
postDate: 2007-04-26T16:15:23.305104-05:00
abstract: Confusion reigns with WPF page navigation...
postStatus: publish
---
26 April 2007

I'm confused...

Reading through the WPF docs it is pretty clear that, when building a page-based WPF app, the WPF container (which looks kind of like a stripped down IE) doesn't keep old page instances in memory. So when you click the back button, previous pages are reloaded.

I found this to be the case with one of my pages, where not only did the page reload, but all the data binding was broken when that occurred. So I had to set KeepAlive to true for that page to make it work. That made some sense to me (though I still don't understand why the data binding within the page was all messed up...)

But now I'm finding that other pages are *not* reloaded. In fact, they are cached in memory, so when I use the Back button to get to them they are showing outdated data.

What a serious pain. I'm sure there are some rules at work behind the scenes here - but I wish the WPF docs were more clear as to what those rules actually were... It appears that the rules are designed to frustrate me: when I want a page to stay in memory it gets reloaded, but when I want a page to reload it stays in memory. Perhaps that's the rule? :)



So the problem I'm trying to resolve right now is this:

I have a page showing Project 123. I then navigate to another page, where I'm able to alter some of the data for Project 123. I then use the Back button to get back to the Project 123 page, but it still shows the old data - making it *very* clear that the page was not reloaded, but rather was cached.

Worse, there doesn't appear to be any nice event raised in a Page object to indicate that it was just navigated to, so I have no way of *forcing* a refresh of the data. That'd be too easy I guess...

Explicitly setting KeepAlive to false has no affect. And I didn't think it would - false is supposed to be the default value.

And I have double-checked to make sure my code doesn't keep any reference to any pages. But I don't: I just create a page object in a method using a local variable and navigate to it using the WPF navigation service.



To be very clear, I actually have a single main page that has a Frame control. My content pages are displayed in this Frame, and my navigation is like this:

\_mainFrame.NavigationService.Navigate(page);

Which does appear to work in all respects, except that page objects are and aren't cached in memory in ways that defy the docs and any rational logic I can see...

Ideas anyone?
