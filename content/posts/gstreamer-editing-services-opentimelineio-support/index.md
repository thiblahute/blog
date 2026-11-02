---
title: "GStreamer Editing Services OpenTimelineIO support"
date: 2019-04-22
slug: gstreamer-editing-services-opentimelineio-support
tags: [gstreamer, ges, opentimelineio, pitivi, igalia, gnome]
guid: https://blogs.gnome.org/tsaunier/2019/04/22/gstreamer-editing-services-opentimelineio-support/
source: wordpress
---

# GStreamer Editing Services OpenTimelineIO support

<a href="https://github.com/PixarAnimationStudios/OpenTimelineIO" class="external">OpenTimelineIO</a> is an Open Source API and interchange format for editorial timeline information, it basically allows some form of interoperability between the different post production Video Editing tools. It is being developed by <a href="http://graphics.pixar.com/" class="external">Pixar</a> and several other studios are contributing to the project allowing it to <a href="https://github.com/PixarAnimationStudios/OpenTimelineIO/commits/master" class="external">evolve quickly</a>.

We, at <a href="https://igalia.com" class="external">Igalia</a>, recently <a href="https://github.com/PixarAnimationStudios/OpenTimelineIO/pull/41" class="external">landed</a> support for the <a href="https://gstreamer.freedesktop.org/data/doc/gstreamer/head/gstreamer-editing-services/html/ges-architecture.html" class="external">GStreamer Editing Services</a> (GES) serialization format in OpenTimelineIO, making it possible to convert GES timelines to any format supported by the library. This is extremely useful to integrate GES into existing Post production workflow as it allows projects in any <a href="https://opentimelineio.readthedocs.io/en/latest/tutorials/adapters.html" class="external">format supported by OpentTimelineIO</a> to be used in the GStreamer Editing Services and vice versa.

On top of that we are building a <a href="https://gitlab.freedesktop.org/gstreamer/gst-editing-services/merge_requests/67" class="external">GESFormatter</a> that allows us to transparently handle any file format supported by OpenTimelineIO. In practice it will be possible to use cuts produced by other video editing tools in any project using GES, for instance <a href="http://www.pitivi.org" class="external">Pitivi</a>:

<video controls preload="metadata" width="512"><source src="screencast.mov" type="video/mp4"><source src="screencast.webm" type="video/webm"></video>

At <a href="https://igalia.com" class="external">Igalia</a> we are aiming at making GStreamer ready to be used in existing Video post production pipelines and this work is one step in that direction. We are working on additional features in GES to fill the gaps toward that goal, for instance we are now implementing <a href="https://gitlab.freedesktop.org/gstreamer/gst-editing-services/issues/60" class="external">nested timeline</a> support and <a href="https://gitlab.freedesktop.org/gstreamer/gst-editing-services/issues/61" class="external">framerate based timestamps</a> in GES. Once we implement them, those features will enhance compatibility of Video Editing projects created from other NLE softwares through OpenTimelineIO. Stay tuned for more information!
