---
title: "GStreamer for video editing (ideas)"
date: 2020-05-08
slug: gstreamer-for-video-editing
tags: [gstreamer, ges, igalia, gnome]
draft: true
---

---
Ideas:
    - GStreamer and its use in the various industries
    - GStreamer is at the core of the main AI framework from industry leaders such
      as nvidia DeepStream SDK
    - Multiplatform framework
    - Supports most formats post processing prod industry requires
        - mxf
        - prores
        - Opentimeline IO
        - Open EXR
    - Very easily extensible, by implementing your own plugins
    - Supports main broadcasting
...

# The motion picture industry and open source software

Historically the motion picture industry has been working with studio specific
tools and methodology and not much technical knowledge was shared between each
others. With the rise of Open Source in the software industry this has started
to change a while back and this trends is goind faster since 2018  when the
Linux foundation started the Academy Software Foundation (aswf).

As developers of the [GStreamer] multimedia framework we have been working on a
piece of technology that is the ready to adopt and adapt for any video
processing and content creationuse cases and we want to make sure you know about
it.

[GStreamer]: https://gstreamer.freedesktop.org

## GStreamer and post production

[GStreamer] is a powerful and versatile open source multimedia
framework that allows creating any kind of media applications. It is deployed in
many industries, ranging from TVs or tiny embedded devices to rendering farms
and broadcasting services. Moreover, it is used as the basis of Deep learning
Sdks such as nvidia' [DeepStream] or Samsung' [nnstreamer] and has over 1550 all
time contributors (~270 per year in the last years).

GStreamer doesn't implement so much of the media processing it performes but
instead leverages any kind of media processing library or tools and allow
application writters to use them all in a comprehensive and efficient way. All
in all, the GStreamer framework focuses on offering a well throught and user
friendly API for all multimedia needs.

Since the beginning of the project, the framework was thought and developed with
the post production use cases needs in mind. As such, the GNonLin plugin was
started in 2001 aiming at providing the basic building block of all Non Linear
editing needs. In the spirit of making simple API for a particular area a new
component has been developed to more easily leverage the framework for video
editing: the [GStreamer Editing Services], GES. This component provides high
level but flexible APIs focused on the Video Editing notions (with objects to
represent the timelines, clips, layers, assets, etc).

GStreamer is multiplatform and official builds are provided for windows, macOS,
android, iOS, and is installed by default in all major linux distribution, as
such, it is the right tool to write multiplatform applications, and this also
applies for post production related applications.


In the last two years, we have been working, here at [Igalia] on implementing
[some](https://blogs.gnome.org/tsaunier/2019/04/22/gstreamer-editing-services-opentimelineio-support/)
[important](https://gitlab.freedesktop.org/gstreamer/gst-editing-services/-/issues/60)
[features](https://gitlab.freedesktop.org/gstreamer/gst-editing-services/-/merge_requests/149)
and fix critical issues in the library as well as in the core of GStreamer to
ensure that GStreamer is ready to be used for advanced post production needs.


[Deepstream]: https://developer.nvidia.com/deepstream-sdk
[nnstreamer]: https://nnstreamer.ai/
[GStreamer Editing Services]: https://gstreamer.freedesktop.org/documentation/gst-editing-services/?gi-language=python