---
layout: post
title: "Reactive Summit 2018 - 1"
description: "Partial lessons learned from a great conference"
category: "scala"
tags: ["programming", "scala", "akka", "streaming", "reactive"]
---

# New or forgotten resources referenced in talks

## Online courses
* Free Lightbend Reactive Architecture courses (for certification):
     * [Introduction to Reactive Principles](https://cognitiveclass.ai/courses/reactive-architecture-introduction/)
     * [Domain Driven Design](https://cognitiveclass.ai/courses/reactive-architecture-ddd/)
     * [Reactive Microservices](https://cognitiveclass.ai/courses/reactive-architecture-microservices/)
     * [Building Scalable Systems](https://cognitiveclass.ai/courses/reactive-architecture-building-scalable-systems/)
     * Not released yet:
          * Distributed Message Patterns
          * Reactive Architecture: CQRS & Event Sourcing

## Papers/Web content
* [Pelkonen, Franklin, Teller et al., Gorilla: A Fast, Scalable, In-Memory Time Series Database, VLDB, 2015](https://www.vldb.org/pvldb/vol8/p1816-teller.pdf)
* Tyler Akidau, The world beyond batch
     * [Streaming 101, 2015](https://www.oreilly.com/ideas/the-world-beyond-batch-streaming-101)
     * [Streaming 102, 2016](https://www.oreilly.com/ideas/the-world-beyond-batch-streaming-102)
* [Knoldus Blog](https://blog.knoldus.com/)
     * e.g. node.js testing with Gatling
     * Welcome, Akka Typed!!

## Books

* [Sean Walsh, Duncan DeVore, Brian Hanafee: Reactive Application Development, Manning, 2018](https://www.safaribooksonline.com/library/view/reactive-application-development/9781617292460/)
* Not published yet: [Francois Garillot, Gerard Maas, Stream Processing with Apache Spark: Best Practices for Scaling and Optimizing Apache Spark, O'Reilly, 2019](https://www.amazon.com/Stream-Processing-Apache-Spark-Optimizing/dp/1491944242)

## Libraries

### Big Data
* [Spark Notebook](https://github.com/spark-notebook/spark-notebook/)

### Performance monitoring, metrics
* [FiloDB time series / event / operational database](https://github.com/filodb/FiloDB)
     * Great keynote on this by Evan Chan, Apple, [@Evanfchan](https://twitter.com/Evanfchan)
* [Riemann distributed systems monitoring](http://riemann.io/)
* [Alexey Ragozin, jvm-tools/Swiss Java Knife](https://github.com/aragozin/jvm-tools)
     * "Small set of tools for JVM troublshooting, monitoring and profiling."
* [Java Microbenchmark Harness](http://openjdk.java.net/projects/code-tools/jmh/)
     * [Kevin Peters, Performance measurement with JMH - Java Microbenchmark Harness, 2017](https://blog.codecentric.de/en/2017/10/performance-measurement-with-jmh-java-microbenchmark-harness/)
* [Influxdata Telegraf](https://github.com/influxdata/telegraf)
     * "plugin-driven server agent for collecting & reporting metrics"

### Reactive Frameworks
* [RSocket (originally from Netflix)](http://rsocket.io/)
     * Polyglot, reactive streams binary protocol

### Around containers
* [Minikube - local Kubernetes](https://kubernetes.io/docs/setup/minikube/)
* [Strimzi - Apache Kafka on OpenShift and Kubernetes](http://strimzi.io/)
