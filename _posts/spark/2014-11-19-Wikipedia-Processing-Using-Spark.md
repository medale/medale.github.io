---
layout: post
title: "Wikipedia Processing Using Spark"
description: "How to process Wikipedia XML dump using Spark"
category: "scala"
tags: ["spark","programming", "scala", "wikipedia"]
---

# How this investigation started...
As a subscriber to the user/dev@spark.apache.org mailing lists I try to keep up
with the activity on the list. When I find something interesting I usually just archive the
email message. But this email thread and subsequent investigation "sparked"
my interest and so I wanted to capture the info and some of the subsequent processing details.

Someone recently asked about "Parsing a large XML file using Spark"
and Tobias Pfeiffer pointed to a great answer in [this reply on mail archive](https://www.mail-archive.com/user@spark.apache.org/msg15776.html).
[Spark Dev message 03520](https://www.mail-archive.com/dev@spark.apache.org/msg03520.html)
shows how they processed the Wikipedia XML dump and the resulting beautiful
http://wikinsights.org with awesome visual graph search features.

# Wikipedia XML Dump
* Following the [official Wikipedia Database Download instructions here](http://en.wikipedia.org/wiki/Wikipedia:Database_download) download
the latest data dump via BitTorrent by clicking on the [the Academic Torrent pages-articles.xml.bz2 listed](http://meta.wikimedia.org/wiki/Data_dump_torrents#enwiki).
At the time of this writing that was the 2014-02-03 version. On my Ubuntu distro that downloaded the 10.59GB file using the Transmission BitTorrent client. 
This took about an hour and presumably conserved some of Wikipedia's bandwidth as compared to the also available direct download link.
* The original email suggested processing via Perl xml_split (see below). Just as a quick investigation I wondered if there
might be a Scala-based tool and came across the [Scales XML Scala library](https://github.com/chris-twiner/scalesXml), which was also linked
from the [Scala Lang Wiki](https://wiki.scala-lang.org/display/SW/Tools+and+Libraries#ToolsandLibraries-XML) and seems active. But my main
investigation was to duplicate what had been alluded to in the email and use Spark, so focused on the Perl approach for now

## xml_split processing
* On my Ubuntu I needed to install xml_split:
    > sudo apt-get install xml-twig-tools

Assuming data dump to $WIKIHOME:
    > cd $WIKIHOME
    > bunzip2 enwiki-20140203-pages-articles.xml.bz2
    > xml_split enwiki-20140203-pages-articles.xml

This created 1833602 split files (little .xml files) in addition to the 
enwiki-20140203-pages-articles.xml.

### Some of the sample files created
```
enwiki-20140203-pages-articles-283772.xml   enwiki-20140203-pages-articles-1235137.xml
enwiki-20140203-pages-articles-1777752.xml  enwiki-20140203-pages-articles-353791.xml
enwiki-20140203-pages-articles-654270.xml   enwiki-20140203-pages-articles-304501.xml
enwiki-20140203-pages-articles-183201.xml   enwiki-20140203-pages-articles-189092.xml
enwiki-20140203-pages-articles-335676.xml   enwiki-20140203-pages-articles-1824038.xml
enwiki-20140203-pages-articles-1336335.xml  enwiki-20140203-pages-articles-1575838.xml
enwiki-20140203-pages-articles-347204.xml   enwiki-20140203-pages-articles-1206186.xml
enwiki-20140203-pages-articles-1134170.xml  enwiki-20140203-pages-articles-689668.xml
enwiki-20140203-pages-articles-439645.xml   enwiki-20140203-pages-articles-1311058.xml
enwiki-20140203-pages-articles-920248.xml   enwiki-20140203-pages-articles-823620.xml
enwiki-20140203-pages-articles-1524113.xml  enwiki-20140203-pages-articles-596755.xml
enwiki-20140203-pages-articles-109698.xml   enwiki-20140203-pages-articles-1663636.xml
```

# Resources
* [The Spark User message that kicked off this investigation](https://www.mail-archive.com/user@spark.apache.org/msg15776.html)
* [The Spark Dev message that shows how they processed the Wikipedia XML dump](https://www.mail-archive.com/dev@spark.apache.org/msg03520.html)
* [The resulting wikiinsights web app](http://wikinsights.org)
