---
layout: page
title: Uebercomputing
tagline: <p>Continuous improvement through project, practices, self</p>
---
{% include JB/setup %}
{% include JB/analytics %}

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


