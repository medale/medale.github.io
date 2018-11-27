---
layout: post
title: "Presentation: Spark Dataframes"
description: "Presentation to the Maryland Apache Spark Meetup"
category: "spark"
tags: ["spark","sql","dataframes","presentation","meetup"]
comments: true
---

The DataFrame abstraction, introduced in Apache Spark 1.3, is a distributed
collection of data organized into named columns. It gives developers a DSL
to expressively manipulate that data while the underlying Catalyst query
optimizer ensures performance. In this presentation for the
[Maryland Apache Spark Meetup](http://www.meetup.com/Apache-Spark-Maryland/events/222996852/)
I provided an overview of the DataFrames API and some sample use cases/comparisons to
RDDs.

Many thanks to Brian Husted, his Tetra concepts team and the [Jailbreak Brewing Company](http://jailbreakbrewing.com/) for organizing and hosting this meetup! Thanks for great
questions and discussions.

## Materials
* [Slides](https://github.com/medale/presentations/blob/master/spark-dataframes-2015/SparkDataFrames.pdf)
* Code available via:

{% highlight bash %}
git clone https://github.com/medale/spark-mail.git
cd spark-mail
git checkout spark-md-meetup-june-2015
mvn clean install

# check sql-analytics/src/main/scala classes for sample code
{% endhighlight %}
