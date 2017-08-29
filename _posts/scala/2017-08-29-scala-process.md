---
layout: post
title: "Scala Process"
description: "Interacting with external programs"
category: "scala"
tags: ["programming", "scala", "process"]
---

Code uses java.nio.file.Files to list all files in the current directory.
Using Scala JavaConverters we convert the Java iterator to a Scala buffer and
the use Process to call unzip on each file.

{% highlight scala%}
import scala.collection.JavaConverters._
import scala.sys.process._
import java.nio.file._
val files = Files.list(Paths.get(".")).iterator.asScala
files.foreach { f => s"unzip $f"! }
{% endhighlight %}

