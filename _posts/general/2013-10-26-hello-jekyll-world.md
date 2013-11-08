---
layout: post
title: "Hello, Jekyll World!"
description: "Getting Jekyll and Jekyll Bootstrap up and running"
category: "general"
tags: [test, general, beginner, jekyll]
---
{% include JB/setup %}

[Jekyll](http://jekyllrb.com/) and [Jekyll Bootstrap](http://jekyllbootstrap.com) are an excellent way
to get a website with blog entries published under your Github repo. Here are some of the lessons learned
while getting things up and running.

## Installation
After cloning the Jekyll bootstrap repo via `git clone https://github.com/plusjade/jekyll-bootstrap.git`
I went to install Jekyll on my Ubuntu 13.10 machine using:

    sudo apt-get install ruby1.9.1-dev
    sudo gem install jekyll

I then tried to run `jekyll serve` from the root directory of the jekyll-bootstrap dir but just got
    
    /usr/bin/jekyll file or directory not found
    
Eventually, trying to run the command as root worked. So I fiddled with permissions on the gems dir and /usr/local/bin/* files but still no joy.

Finally, as user I tried the rvm route I found in [this article](https://www.digitalocean.com/community/articles/how-to-get-started-with-jekyll-on-an-ubuntu-vps):

    curl -L https://get.rvm.io | bash -s stable --ruby=2.0.0
    
That did the trick (and I now have a newer Ruby)
