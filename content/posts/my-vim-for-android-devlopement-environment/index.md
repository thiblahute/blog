---
title: "My vim for android devlopement environment"
date: 2009-11-22
slug: my-vim-for-android-devlopement-environment
guid: https://thiblahute.blogspot.com/2009/11/my-vim-for-android-devlopement.html
source: blogger
---

I haven't blogged for a long time, and I would have liked to be able to blog about [my Gnome soc project](http://thiblahute.blogspot.com/2009/08/gsoc-add-google-documents-support-to.html), but unfortunately, I have other priorities. As part of my studies, I had to do some development for the android platform, and since the last summer, I can't use other development environment than Vim, I decided to find a way of using it for my android project.  

So here is the description of my Vim environment for android applications development. I use vim 7.2, the version distributed with Ubuntu 9.10, the [Vjde plugin](http://www.vim.org/scripts/script.php?script_id=1213), [terminator](https://launchpad.net/terminator) as a terminal (which by the way is a great terminal emulator!!) and then [last android JDK](http://developer.android.com/sdk/index.html) in order to develop application for android2.0 (eclaire).  

First I installed the SDK (there are a few bugs on the emulator installation due to [this bug](https://bugzilla.gnome.org/show_bug.cgi?id=598734) and an [this ssl problem.](http://groups.google.com/group/android-developers/browse_thread/thread/814e3c898d7b24fc?hl=en#) I fallowed [this guide](http://developer.android.com/sdk/index.html) to set the sdk. Then, I installed the Vjde plug-in which is a Vim plug-in to get a Java development environment in Vi, this plugin permit to add intelligent completion for methods calls as well as for imports (I only unziped [this](http://www.vim.org/scripts/download_script.php?src_id=10992) in you ~/.vim directory). Afterward, I created my android project ([this](http://developer.android.com/guide/developing/other-ide.html) page explains well how to do it). And then I created an vjde project, in vim:  
  
`:Vjdeas filename.prj`  
  
This is actually a text file which permit to save variables to you project. Then I set it Vjde to look at android class, methods and package, in vim:  
  
`:let g:vjde_lib_path='/path/to/android/sdk/platforms/android-2.0/android.jar:build.classes'`  
  
And save it  
  
`:Vjdesave`  
  
Thanks to it, I can have functions/imports completion available with the CTRL-X+CTRL-U key combination (I need to load the project(<span style="font-style: italic;">:Vjdeload filename.prj)</span> every time I want to work on it, I think there must be a way of doing it automatically but didn't figure it out yet). It would also be possible to get the documentation integration thanks to the Vjde plugin, but I am used to have it in another window.  
  
Then to try the program on the android emulator, I lunch the emulator, and in a terminal:  
  
`ant debug && adb install -r bin/yourAppName-debug.apk`  
  
You can then launch it in the android emulator menu (I looked for a way of lunching the program directly from the command line, but didn't find :( ). To debug the app, you can launch the [ddms](http://developer.android.com/guide/developing/tools/ddms.html) tool which is part of the android sdk.

I hope this could be useful for some people who want to develop for the android platform and don't want to use eclipse or netbeans IDE.

  
  
Edit: I find a good trick to manage the make and install thing, base from [here](http://www.builderau.com.au/program/java/soa/Configure-vi-for-Java-application-development/0,339024620,320276164,00.htm). I added the following (executable) file to ~/.local/bin/vimAntAndroid:  
  
`#!/bin/sh`  
`ant debug -Dbuild.compiler.emacs=true -quiet -find build.xml 2>&1 | grep '\[javac\]'`  
`echo "Installing..."`  
`adb install -r ${1} | grep 'null'`  
And then in Vim  
  
`set makeprg=vimAntAndroid`  
