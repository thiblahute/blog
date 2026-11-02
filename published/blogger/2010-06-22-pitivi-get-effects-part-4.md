---
title: "Pitivi get effects, part 4"
date: 2010-06-22
url: https://thiblahute.blogspot.com/2010/06/pitivi-get-effects-part-4.html
---

<div style="text-align: justify;">

I didn't blog for almost 2 weeks now because I wanted to have something interesting to say before saying it!  
  
So the last 2 weeks I started an [experimental branch](http://github.com/thiblahute/Pitivi/tree/experimental-timeline-based) to handle effects in the timeline and of course corrected all the bugs I found during this time. Then I rethought this design with [nekohayo](http://jeff.ecchi.ca/blog/) and got this pretty cool mockup from him:  

</div>

  
<a href="http://lh6.ggpht.com/_3mLd5CtlHo4/TCIk1jYJH3I/AAAAAAAAHSw/J_ELnMPOmQE/s1152/Capture-3.png" onblur="try {parent.deselectBloggerImageGracefully();} catch(e) {}"><img src="http://lh6.ggpht.com/_3mLd5CtlHo4/TCIk1jYJH3I/AAAAAAAAHSw/J_ELnMPOmQE/s1152/Capture-3.png" style="display: block; margin: 0px auto 10px; text-align: center; cursor: pointer; width: 460px; height: 288px;" data-border="0" /></a> So as you can expect, I am now implementing that. I already rewrite the effect list and it looks the same as you can see in the mockup. And I am working on making effects being per clip or per track instead of being considered as clips themselves. This should actually be pushed by the end of the week.  
  
So afterward I am going to work on this new middle section for clips properties and effect configurations. I think I will get it working in the next two weeks. I am quite in advanced on the planning I proposed for the postulation but this is a good thing because I am still at university and may have to spend more time for it in the coming weeks.  
  
You still can grab my latest code [here](http://github.com/thiblahute/Pitivi) and play with it!
