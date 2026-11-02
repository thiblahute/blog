---
title: "Pitivi is getting effects, Part 1"
date: 2010-05-14
slug: pitivi-is-getting-effects-part-1
guid: https://thiblahute.blogspot.com/2010/05/pitivi-is-getting-effects-part-1.html
source: blogger
---

<span class="Apple-style-span" style="font-family:'DejaVu Sans', sans-serif;"><span class="Apple-style-span" style="font-size:medium;"> </span></span>

<span class="Apple-style-span" style="font-family:'DejaVu Sans', sans-serif;"></span>

<span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="background: transparent"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-style: normal">Here is the first report about [my Google summer of code project](http://thiblahute.blogspot.com/2010/04/i-have-been-accepetd-for-google-summer.html). I have been working quite a lot on it for the last 2 weeks! So here is the summary of what have been done so far:</span></span></span></span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span lang="en-US"><span style="font-style: normal"><span style="font-weight: normal"><span style="background: transparent">Code reading, analyze of Pitivi architecture (Thanks to the [pitivi wiki](http://wiki.pitivi.org/wiki/Main_Page)</span></span></span></span></span></span></span><span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="font-style: normal"><span style="font-weight: normal">)</span></span></span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;">Some reading about Gstreamer to understand better the way it works</span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;">Creation of [my git branch](http://github.com/thiblahute/pitivi) to start working on effects implementation</span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="background: transparent">Implementation of the core Pitivi modifications to be able to create effects (With unit tests)</span></span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span lang="en-US"><span style="font-style: normal"><span style="font-weight: normal"><span style="background: transparent">See how I can implement [effect files](http://live.gnome.org/AppIntegration/GstreamerVisualEffects) as </span></span></span></span></span></span></span><span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="font-style: normal"><span style="font-weight: normal">described in my Gsoc application, and discussions about it in the Pitivi community. We actually didn't take a fixed decision about this for now.</span></span></span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span lang="en-US"><span style="font-style: normal"><span style="font-weight: normal"><span style="background: transparent">Creation of the UI to show the list of effects detected thanks to the [gstreamer registry](http://www.gstreamer.net/data/doc/gstreamer/head/gstreamer/html/GstRegistry.html) (the list was already retrieved in Pitivi)</span></span></span></span></span></span></span>

- <span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="background: transparent"><span style="font-style: normal">Some talking to know how this UI should be done. I will need to talk more about that to the Pitivi community to take a good decision about how it should look like. For now, it looks like:</span></span></span></span></span>

<a href="9cea4b-first_screenshot.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img src="ced6d2-first_screenshot.png" id="BLOGGER_PHOTO_ID_5471340830349008834" style="display:block; margin:0px auto 10px; text-align:center;cursor:pointer; cursor:hand;width: 320px; height: 200px;" data-border="0" /></a>

<span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="background: transparent">I am now working on drag'n droping effects to the timeline.</span></span></span></span>

<span style="color:#000000;"><span style="font-family:DejaVu Sans, sans-serif;"><span style="font-size:100%;"><span style="background: transparent">That is all for now, and I will give you frequent news about how things are going.</span></span></span></span>
