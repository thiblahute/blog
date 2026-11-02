---
title: "Frame accuracy in GStreamer Editing Services"
date: 2020-05-08
slug: gstreamer-frame-accuracy
tags: [gstreamer, ges, igalia]
draft: true
---


In [Igalia' effort] to make the [GStreamer] framework ready for post production
and in particular for Video Editing use cases, we need to make sure that the
framework is precise to the frame. Therefore we have been ensuring
that it is possible to reference frames precisely, generically in GStreamer, and
in particular in the [GStreamer Editing Services].

This work consisted in several 

[GStreamer]: https://gstreamer.freedesktop.org/documentation/
[Igalia' effort]: https://blogs.gnome.org/tsaunier/2019/04/22/gstreamer-editing-services-opentimelineio-support/
[GStreamer Editing Services]: https://gstreamer.freedesktop.org/documentation/gst-editing-services/

## The notion of time in GStreamer

GStreamer references all times in nanosecond as [GstClockTime] as opposed to
what other framework and libraries such as [ffmpeg] or [AVFoundation] do, which
is referencing time as rational times, allowing to specify a time scale, and
avoiding rounding errors. This is a design choice and both solutions have their
pros and cons, but this is out of scope for that blog post.


## Seeking in GStreamer

Inside the pipeline, the "region of interest" is defined using the [GstSegment]
structure, it basically defines the part of the media file needs to be reprduced
and at what playback speed. This is basically configured by the user using the
[seek GstEvent] where we can also pass [flags] to request specific behaviour
during the seek as well as the 'precision' of the seek, by requesting an
[`accurate`](GST_SEEK_FLAG_ACCURATE) and knowing the framerate of the input
media, we should be able to seek to a specific frame.

Note that GStreamer also has the notion of [default format] which aims at
allowing to make the timing value refer to a media sepcific unit. For example,
for the video case, it would be a number of frames/images, for the audio case,
it would be the number of samples/frames (samples per channel). Theorically it
can be used to seek in frame number, in practice it is not well support and an
issue with it is that it won't work in the case of Video Editing where we might
work with assets that

[GstClockTime]: https://gstreamer.freedesktop.org/documentation/gstreamer/gstclock.html?gi-language=c#GstClockTime
[ffmpeg]: https://ffmpeg.org
[AVFoundation]: https://developer.apple.com/documentation/avfoundation
[GstSegment]: https://gstreamer.freedesktop.org/documentation/gstreamer/gstsegment.html
[seek GstEvent]: https://gstreamer.freedesktop.org/documentation/gstreamer/gstevent.html#gst_event_new_seek
[flags]: https://gstreamer.freedesktop.org/documentation/gstreamer/gstsegment.html#GstSeekFlags
[default format]: https://gstreamer.freedesktop.org/documentation/gstreamer/gstformat.html?gi-language=python#members-1