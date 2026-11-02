---
title: "First post: My google Summer of code project and my future in the gnome comunity"
date: 2009-08-05
slug: first-post-my-google-summer-of-code-project-and-my-future-in
tags: [gnome, gsoc]
guid: https://thiblahute.blogspot.com/2009/08/first-post-my-google-summer-of-code.html
source: blogger
---

<div style="text-align: justify;">

This is my first post on a blog, I decided to write now about my Gsoc project, "Nautilus: add support to Google documents" because it's almost the end of this project and because I decided that I want to carry on this work. As you may have heard about, this project consist in adding the possibility to nautilus users to use their [Google documents](http://docs.google.com/) as if they were local documents so it mean that they should be able to use it with any office application suite such as Open-office, Goffice... This will permit users to always have their documents synchronized on the web and to be able to access it on-line (throw the Google website) all the time even if they can manage it very easily from their computer and use it with their favorite software.  
  
To complete this project I had to work on three different gnome project which are:  

</div>

- Libgdata: A Glib base library which permit to handle Google services. I needed to hack on it to add the Google documents services. The service is now implemented and available in the master branch of the [git](http://git.gnome.org/cgit/libgdata/) repository.
- GVFS: the gnome virtual file system. I needed to add a Google documents backend which permits to handle the Google documents with any program using it. I now have a branch accessible [here](http://github.com/thiblahute/gvfs/tree/googledocuments). It is not finalized yet but in a good way. I will need some review in the coming days ;)  
- Nautilus: done, patch available [here](http://bugzilla.gnome.org/show_bug.cgi?id=591178).  

<div style="text-align: justify;">

I think I will use this blog to talk about my gnome hackes and I won't stop working on gnome after my Google summer of code since I enjoyed a lot the work I did so far and even if I couldn't be at GUADEC this year I wish I could next year ;)  
  
I first want my Gsoc project to be integrated in gnome (maybe 2.30/3.0? would be great for me ;) ) I know I need to get it working perfectly before, and to polish it a lot... but I will do it. I also will add some feature such the possibility to access documents off-line and synchronize it when the user get connected. And maybe more when I get more ideas!  
  
And afterward I have some other projects such as the creation of another backend to access Google Picassaweb pictures, I actually have thought my actual Backend so it will be more simple to integrate this other one.

</div>
