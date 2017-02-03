---
title: BroadcastChannel API
date: 2016-09-19 20:28:50
tags: JavaScript, Browser APIs
---

Early last week, Chrome posted the new features coming in Chrome 54. One of the features that stood out was Broadcast channel.  This API facilitates communicate with other windows, tabs, and service workers running within the same origin.  It sounds oddly familiar to window.postMessage API, which allows you to do the same window to window communication.  The big difference here is, window.postMessage requires you to maintain a reference to the window you want to communicate with.

```javascript
var popup = window.open('https://www.coolwebsite.com');
popup.postMessage('Hello From Dev Boostie!');
```

We all know maintaining references to windows is hard, right?  If you’re not accustomed to it, the process goes something like this.  Open a window, register it with an in memory collection.  When the window closes, send an event to the parent and cleanup the reference.  While it doesn’t sound too bad, managing these window references can become a serious pain and it’s tough to get right.

Thankfully BroadcastChannel API solves this.  It provides the ability to send messages to all windows/tabs without knowledge of their existence.  No more in memory window management!

The one downside to the BroadcastChannel API is it only works with same origin.  If you want two windows to communicate with each other window.postMessage is the way to go.

For more on the BroadcastChannel API checkout this blog post from Google.

BroadcastChannel API Browser Support

Can I Use broadcastchannel? Data on support for the broadcastchannel feature across the major browsers from [caniuse.com](http://caniuse.com/#feat=broadcastchannel).