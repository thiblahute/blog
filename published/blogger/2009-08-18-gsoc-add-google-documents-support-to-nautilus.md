---
title: "Gsoc: add google documents support to nautilus"
date: 2009-08-18
url: https://thiblahute.blogspot.com/2009/08/gsoc-add-google-documents-support-to.html
---

<div>

<div style="text-align: justify;">

During those 12 weeks of my Google summer of code, I have hacked mainly on 2 gnome project which are gvfs and libgdata.

</div>

<div style="text-align: justify;">

  

</div>

<div style="text-align: justify;">

Concerning libgdata, I added the google documents service and it's now in the master branch, it's functional even if there are still a few bugs.

</div>

<div style="text-align: justify;">

  

</div>

<div style="text-align: justify;">

As far as gvfs is concerned, I have an alpha version of the gdocs backend which isn't really usable for final users yet, but don't worry I am going to make it working well in the coming weeks! All the functions are implemented, I need to stabilize it and optimize it in order to hopefully get it merged in gvfs.

</div>

<div style="text-align: justify;">

  

</div>

<div style="text-align: justify;">

I have also worked a little bit on nautilus to support the new backend (almost nothing).

</div>

some screenshots:

</div>

<a href="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEFsvSXq4-h8Dd8L4qPPkvs9TuvSyO_w4Fdfqu1catjln8w7_9n8HAd_2GSEU8BOwkaz1hyphenhyphenmj4Vx047-Nv5MnQvM1Lyv2KAdMQuhHPRI8DEoKz7gAEPhsnyjedrI9uaPo22rZYv7VmYLU/s1600-h/show_google_documents.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiEFsvSXq4-h8Dd8L4qPPkvs9TuvSyO_w4Fdfqu1catjln8w7_9n8HAd_2GSEU8BOwkaz1hyphenhyphenmj4Vx047-Nv5MnQvM1Lyv2KAdMQuhHPRI8DEoKz7gAEPhsnyjedrI9uaPo22rZYv7VmYLU/s320/show_google_documents.png" id="BLOGGER_PHOTO_ID_5371405685229221906" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; width: 320px; height: 200px;" data-border="0" /></a>  
<a href="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihaUJLXxo8C0g-7EoxQaI2nRxvHjPknhE0aqLcJMXvD0klPD5275N3xsSGYl2Kp2rERtn_Ns093Al0f79h5-H7cYS_qmQTR4Pl6laWKDjouhEUN7Ihpt8aNYB6lNw9tOHRy4Qe5aZxrzM/s1600-h/Connecting_window.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEihaUJLXxo8C0g-7EoxQaI2nRxvHjPknhE0aqLcJMXvD0klPD5275N3xsSGYl2Kp2rERtn_Ns093Al0f79h5-H7cYS_qmQTR4Pl6laWKDjouhEUN7Ihpt8aNYB6lNw9tOHRy4Qe5aZxrzM/s320/Connecting_window.png" id="BLOGGER_PHOTO_ID_5371405681095447314" style="margin: 0px auto 10px; display: block; text-align: center; cursor: pointer; width: 320px; height: 200px;" data-border="0" /></a>

<div>

<div style="text-align: left;">

  

</div>

<div style="text-align: left;">

If you anyway want to give it a try (I think you should wait a few weeks more), you will need:

</div>

<div style="text-align: left;">

- [Libgdata master branch](http://git.gnome.org/cgit/libgdata/tree/gdata/).
- [My Gvfs branch.](http://github.com/thiblahute/gvfs/tree/googledocuments)
- The latest nautilus and optionality [my patch](http://bugzilla.gnome.org/show_bug.cgi?id=591178) for a better integration of the new GVFS backend.

</div>

</div>
