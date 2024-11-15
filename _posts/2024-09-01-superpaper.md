---
title: 'How I spent 2 years to over-engineer a solution to a minor inconvenience'
date: 2024-09-01
permalink: /posts/2024/09/superpaper
tags:
 - programming
 - python
---

<img src='/images/superpaper-drake-no-yes.jpg'>

A story of me wanting an application for GNU/Linux, so I learned Python to write it myself
======
Early 2019 I decided to switch my home PC to Linux, however I couldn't find a good enough replacement for DisplayFusion, my multi-monitor tool of choice on Windows. I took a look at Nitrogen, Hydrapaper, and Syncwall which seem to be the common recommendations. However I wanted the tool to:
    - span image across all monitors
    - set different images on monitors
    - do timed slideshow
    - support KDE Plasma
    - and a bonus would be: support hotkeys (or be scriptable to enable me to do this)
Unfortunately none of the popular options do all of the above; and as far as I can tell, none of them support spanning images on KDE Plasma. Supporting Plasma turned out to be a bit troublesome but doable, as we'll find out.

So I quickly cobbled together a proof of concept to see if I could do it (multi image wallpaper at this point) and it did seem doable. Superpaper 1.0 was a command-line only utility that needed to be configured with preference files. Around this time I realized that since I'm building the tool from ground up, I can fix an issue that I had had with multi-monitor wallpaper spanning for a long time. You see my two displays have always been slightly different size and resolution. This means that their pixel sizes are not equal and this then means that the wallpaper image is not scaled identically on the displays, and this breaks the alignment of the span. A new feature to implement! Now I wanted to replace DisplayFusion on Windows as well.

Early summer 2019 I had an implementation of this pixel density correction that also could take display bezels into account for even better spanning, and so I released Superpaper 1.1 with a rudimentary GUI as a portable package. However the pixel density and bezel feature could not handle displays in arbitrary arrangements, only a row of displays. This was unsatisfactory, but I didn't know how to fix it at the time.

During Christmas holidays I came up with a solution to the issue; it required a large overhaul of multiple things. I needed to ask the user to tell how their displays are actually positioned on their table to be able to tell where their pixels of different sizes actually are positioned, since the resolution information from the OS does not tell this. With this information I could make the image shown on the displays span beautifully. I had to redesign the wallpaper algorithm to support this new data, and support bezels on top and bottom edges as well, in addition to on the sides.

While working on all these improvements I realized one last missing piece of the spanning problem. You see even when the image is scaled correctly on the different displays, there was still an imperfection with the produced wallpaper. Horizons, mountain ranges, water surfaces etc looked bent when comparing the images across the display boundary. I realized that this happens because the displays are rotated to face the viewer. If they were flat against a wall this issue doesn't come up. Designing a fix to this perspective issue took a while; and I wouldn't have ever guessed to get to use some of the same maths that self-driving cars use to see in my wallpaper tool.. I wanted to compute what the wallpaper image has to look like so that it seems that it is a one flat image running behind all the displays. This would fix the bent/cut lines/shapes. The solution uses the maths with which robotic vision reconstructs a flat surface in 3D from a camera image; a road surface for example. I wrote a bit of a wiki page demonstrating this in action: [here](https://github.com/hhannine/superpaper/wiki/Wallpaper-spanning-with-advanced-options:-what-the-pixel-density-and-perspective-corrections-are-about). 

Since then I've added a couple of features such as [MacOS support](https://github.com/hhannine/superpaper/releases/tag/v2.2.0), and support for spanning wallpapers on display groups.

Superpaper is open source, supports Windows, GNU/Linux and MacOS, and is available for free on [GitHub](https://github.com/hhannine/superpaper/).

<img src='/images/gui-screenshot.png'>

This writeup is largely based on my previous [post on the topic on Reddit](https://www.reddit.com/r/linux/comments/g6l5lj/superpaper_200_i_wrote_a_multimonitor_wallpaper/), with a little update at the end.
