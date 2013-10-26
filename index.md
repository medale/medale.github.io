---
layout: page
title: Uebercomputing
tagline: Continuous improvement through project, practices, self
---
{% include JB/setup %}

Just getting started...
    
## Thoughts, observations and other random phenomena

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

## Miscellaneous

### Links
* [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)

<h2>About</h2>
   <ul>
     <li class="contact">M. Dale: medale at acm.org</li>
     <li class="github"><a href="http://github.com/medale/" rel="me">github.com/medale</a></li>
     <li class="twitter"><a href="http://twitter.com/medale94/" rel="me">twitter.com/medale94</a></li>
   </ul>
