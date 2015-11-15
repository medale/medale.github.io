---
layout: post
title: "Linux Movie Editing Tools"
description: "Posting a presentation to YouTube - Linux tools that help"
category: "opensource"
tags: [linux, movie, youtube]
---

# Background
On April 22nd, 2015, I had the privilege of giving a presentation on
"Adding Spark to Your Hadoop" to the [Baltimore Hadoop User Meetup Group](http://www.meetup.com/Baltimore-Hadoop-User-Group/events/221583743/)
at the wonderful AOL spaces on McDonnell Street at Brewers Hill.

We captured the presentation on video but it was impossible to read the
slides or follow the demo. So I needed to do some video work to splice in the
slides and smaller desktop-captured demos. The result is uploaded to YouTube [here](https://www.youtube.com/watch?v=WgqYn3RlWlI).

# Open source Tools Used

Once again the open source community made this project relatively easy for
someone who had no background in video editing. After some internet searching
I selected the following tools:

1. [OpenShot Video Editor](http://www.openshot.org/) - create and export video
1. [Poppler-utils pdftoppm](http://poppler.freedesktop.org/) - export PDF slides to PNGs
1. [Kazam Screencaster](https://code.launchpad.net/kazam) - record desktop demo
1. [Shutter Screenshot Tool](http://shutter-project.org/) - capture screen shots

## Exporting PDF slides to PNG

At first, I used Shutter to take screenshots of each slide but realized
quickly that some automation was needed. [This AskUbuntu answer](http://askubuntu.com/questions/50170/how-to-convert-pdf-to-image/50180#50180) provided the solution:

{% highlight bash %}
sudo apt-get install poppler-utils
pdftoppm -rx 300 -ry 300 -png presentation.pdf prefix
{% endhighlight %}

## OpenShot

1. Added the original mpeg recording to Project files/video
1. Created a title (this became Track 1)
1. Added the mpeg (Track 2) right after the title
1. Import all slides as PNGs (Image - right-click - Import Files)
1. As relevant slides come up, use "Add marker" to mark the start
1. Add PNG slides and desktop movies at their markers
1. Use audio from the mpeg recording

Once done:

1. File - Export Video - Profile Web
1. Target: YouTube-HD
1. Video Profile: HD 720p 25fps
1. Quality High

## YouTube
Until verified, YouTube limits a user to 15 minute video
length. After uploading the long video there was a link to verify identity. After upload the video was available on YouTube [here](https://www.youtube.com/watch?v=WgqYn3RlWlI).
