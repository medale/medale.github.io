---
layout: page
title: Uebercomputing
tagline: Continuous improvement through project, practices, self
---
{% include JB/setup %}

Just getting started...
    
## Thoughts, observations and other somewhat random phenomena

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## Some of my Github Projects
* [Jexsiter - md5hash of ssl directory with Git-backed local backups](https://github.com/medale/JexSiter)
* [Scala Musings - exploring Scala after completing Martin Odersky's Functional Programming MOOC at Coursera](https://github.com/medale/scala-musings)
* [ANTLR4 - Learned more about the power of Terence Parr's great parser generator tool](https://github.com/medale/antlr4-experiments)
* [WhyMi - An Android-based survey tool created as part of the Americas Datafest DC by the awesome AppNewbs](https://github.com/medale/WhyMi)

### Links
* [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

<h2>About</h2>
   <ul>
     <li class="contact">Markus Dale: medale at acm.org</li>
     <li class="github"><a href="http://github.com/medale/" rel="me">github.com/medale</a></li>
     <li class="twitter"><a href="http://twitter.com/medale94/" rel="me">twitter.com/medale94</a></li>
   </ul>
