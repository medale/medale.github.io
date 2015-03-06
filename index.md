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
  {% capture currentyear %}{{post.date | date: "%Y"}}{% endcapture %}
  {% if currentyear != year %}
    {% unless forloop.first %}</ul>{% endunless %}
    <h3>{{ currentyear }}</h3>
    <ul>
    {% capture year %}{{currentyear}}{% endcapture %}
  {% endif %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  {% if forloop.last %}</ul>{% endif %}
 {% endfor %}
</ul>

## Some of my Github Projects
* [Spark Mail - Tutorial for using Spark to process Enron Email dataset](https://github.com/medale/spark-mail)
* [Spark Mail Docker image](https://github.com/medale/spark-mail-docker) - Docker image to accompany Spark Mail Tutorial (Spark 1.2.1 on Hadoop 2.6.0 with subset of Enron email in avro format)
* [Extension Sorter](https://github.com/medale/extension-sorter) - sort files into new destination by their file extensions (configurable)
* [Jexsiter - md5hash of ssl directories with Git-backed local backups](https://github.com/medale/JexSiter)
* [Scala Sampler - exploring Scala after completing Martin Odersky's Functional Programming MOOC at Coursera](https://github.com/medale/scala-sampler)
* [ANTLR4 - Learned more about the power of Terence Parr's great parser generator tool](https://github.com/medale/antlr4-experiments)

### Links
* [Apache Spark Nuggets](/spark.html)
* [Data Science Research](/dataScience.html)
* [Linux Commands](/linuxCommands.html)
* [Links Repo](/links.html)
* [Memory Pad](/memory.html)
* [Musik](/musik/musik.html)
* [Jekyll Quick Start](http://jekyllbootstrap.com/usage/jekyll-quick-start.html)
