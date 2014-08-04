Title: Tracking EME implementation on Firefox
Date:  2013-12-27
Category: learning
Tags: encrypted media extention, eme, drm, firefox, adobe, HTML5, mozilla

As you might know, Mozilla officially announced months ago that it will begin to implement the Encrypted Media Extension (EME) HTML5 specification for Firefox, that allows DRM content on video and audio. This wasn't an easy decision, since Mozilla is always trying to keep the web as open as possible.

Unlike other browsers, Mozilla decided to not implement directly the component and opted for a third-party plugin implementation running within an opensource sandbox. (more details : https://hacks.mozilla.org/2014/05/reconciling-mozillas-mission-and-w3c-eme/ )

So if you are worried about how mozilla is going to implement EME, There is A meta bug on [bugzilla](https://bugzilla.mozilla.org) used to reference to all bugs related to the spec implementation that you can track.
(PS: for mozilla a bug can be anything, an issue, a new feature, a discussion ...)

[[EME][META] Implement Encrypted Media Extensions ](https://bugzilla.mozilla.org/show_bug.cgi?id=1015800)

You will find the referenced bugs in the "Depends on" section :

![Meta bug](http://i.imgur.com/RqYQsef.png)

If you want to be notified about any bug updates you can create a bugzilla account, pick a bug on which you are interested in and add yourself to "CC List" and then save the changes

![Subscrive CC list](http://i.imgur.com/QhSGxfE.png)
