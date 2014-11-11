---
layout: post
title: "Incremental Scala compilation with Zinc"
description: "How to use Zinc to increase compilation speed for Scala"
category: "scala"
tags: ["programming", "scala", "sbt", "maven"]
---
{% include JB/setup %}

# What is Zinc
Zinc is a standalone version of the [incremental compiler for sbt GitHub page](https://github.com/typesafehub/zinc). 
Providing a "warmed-up" JVM it increases compilation speed. The [scala-maven-plugin](http://davidb.github.io/scala-maven-plugin/example_incremental.html)
allows us to take advantage of incremental compilation from a Maven build.

Follow the link on the Zinc GitHub page to download latest stable version and
install.

# Running zinc
```bash 
cd $ZINC_DIR/bin
./zinc -scala-home /usr/local/scala-2.10.4 -start
./zinc -status       #After compilation shows cached setup
./zinc -shutdown
```
# Enable Zinc from scala-maven-plugin
 
```xml
<plugin>
   <groupId>net.alchim31.maven</groupId>
   <artifactId>scala-maven-plugin</artifactId>
   <version>3.2.0</version>
   <executions>
	...
   </executions>
   <configuration>
      <scalaVersion>${scala.version}</scalaVersion>
      <recompileMode>incremental</recompileMode>
      <useZincServer>true</useZincServer>
	...
```
		
# Resources
* [Typesafe Zinc GitHub](https://github.com/typesafehub/zinc)
* [Typesafe blog Incremental compilation with Zinc](http://typesafe.com/blog/zinc-and-incremental-compilation)
* [Scala Maven Plugin](http://davidb.github.io/scala-maven-plugin/example_incremental.html)
