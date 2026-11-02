---
title: "GStreamer: one repository to rule them all"
date: 2021-09-29
slug: gstreamer-one-repository-to-rule-them-all
tags: [gstreamer, meson, build-system]
guid: https://blogs.gnome.org/tsaunier/2021/09/29/gstreamer-one-repository-to-rule-them-all/
source: wordpress
---

For the last years, the <a href="https://gstreamer.freedesktop.org/" class="external" target="_blank" rel="noopener">GStreamer</a> community has been <a href="https://gitlab.freedesktop.org/gstreamer/gstreamer/-/issues/474" class="external">analysing and discussing</a> the idea of merging all <a href="https://gstreamer.freedesktop.org/documentation/additional/splitup.html" class="external" target="_blank" rel="noopener">the modules</a> into one single repository. Since all the official modules are released in sync and the code evolves simultaneously between those repositories, having the code split was a burden and several core GStreamer developers believed that it was worth making the effort to consolidate them into a single repository. As <a href="https://lists.freedesktop.org/archives/gstreamer-devel/2020-November/076754.html" class="external" target="_blank" rel="noopener">announced</a> a while back this is now effective and this post is about explaining the technical choices and implications of that change.

You can also check out our <a href="https://gstreamer.freedesktop.org/documentation/frequently-asked-questions/mono-repository.html" class="external" target="_blank" rel="noopener">Monorepo FAQ</a> for a list of questions and answers.

## Technicall details of the unification

Since we moved to <a href="https://mesonbuild.com/" class="external" target="_blank" rel="noopener">meson</a> as a build system a few years ago we implemented <a href="https://gitlab.freedesktop.org/gstreamer/gst-build/-/tree/29352ad0f82c38649424801c97473e33d75caf41" class="external" target="_blank" rel="noopener">gst-build</a> which leverages the <a href="https://mesonbuild.com/Subprojects.html" class="external">meson subproject</a> feature to build all GStreamer modules as one single project. This greatly enhanced the development experience of the GStreamer framework but we considered that we could improve it even more by having all GStreamer code in a single repository that looks the same as `gst-build`.

This is what the new unified git repository looks like, `gst-build` in the main `gstreamer` repository, except that all the code from the GStreamer modules located in the `subprojects/` directory are checked in.

This new setup now lives in the `main` default branch of <a href="https://gitlab.freedesktop.org/gstreamer/gstreamer/-/tree/main" class="external" target="_blank" rel="noopener">the gstreamer repository</a>, the `master` branches for all the other modules repositories are now retired and frozen, no new merge request or code change will be accepted there.

This is only the first step and we will consider reorganizing the repository in the future, but the goal is to minimize disruptions.

The technical process for merging the repositories looks like:

    foreach GSTREAMER_MODULE
        git remote add GSTREAMER_MODULE.name GSTREAMER_MODULE.url
        git fetch GSTREAMER_MODULE.name
        git merge GSTREAMER_MODULE.name/master
        git mv list_all_files_from_merged_gstreamer_module() GSTREAMER_MODULE.shortname
        git commit -m "Moved all files from " + GSTREAMER_MODULE.name
    endforeach

This allows us to keep the exact same history (and checksum of each commit) for all the old gstreamer modules in the new repository which guarantees that the code is still exactly the same as before.

## Releases with the new setup

In the same spirit of avoiding disruption, releases will look **exactly the same** as before. In the new unique `gstreamer` repository we still have meson subprojects for each GStreamer modules and they will have their own release tarballs. In practice, this means that not much (nothing?) should change for distribution packagers and consumers of GStreamer tarballs.

## What should I do with my pending MRs in old modules repositories?

Since we can not create new merge requests in your name on gitlab, we wrote a <a href="https://gitlab.freedesktop.org/gstreamer/gstreamer/-/blob/main/scripts/move_mrs_to_monorepo.py" class="external" target="_blank" rel="noopener">move_mrs_to_monorepo</a> script that you can run yourself. The script is located in <a href="https://gitlab.freedesktop.org/gstreamer/gstreamer/-/tree/main" class="external" target="_blank" rel="noopener">the gstreamer repository</a> and you can start moving all your pending MRs by simply calling it (`scripts/move_mrs_to_monorepo.py` and follow the instructions).

------------------------------------------------------------------------

You can also check out our <a href="https://gstreamer.freedesktop.org/documentation/frequently-asked-questions/mono-repository.html" class="external" target="_blank" rel="noopener">Monorepo FAQ</a> for a list of questions and answers.

Thanks to everyone in the community for providing us with all the feedback and thanks to <a href="https://blogs.gnome.org/xclaesse/" target="_blank" rel="noopener">Xavier Claessens</a> for co-leading the effort.

We are still working on ensuring the transition as smoothly as possible and if you have any question don’t hesitate to come talk to us in \#gstreamer on the oftc IRC network.

Happy GStreamer hacking!
