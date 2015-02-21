---
layout: post
title: "Spark On Docker"
description: "How to run Spark on Docker"
category: "spark"
tags: ["spark","docker"]
---
{% include JB/setup %}

# Installing Docker on Ubuntu
* [Docker on Ubunutu](https://docs.docker.com/installation/ubuntulinux/)

# Running Spark 1.2 Docker

* [SequenceIO - Spark 1.2.0 on Docker](http://blog.sequenceiq.com/blog/2015/01/09/spark-1-2-0-docker/)
* https://github.com/sequenceiq/docker-spark


    sudo docker pull sequenceiq/spark:1.2.0
    sudo docker run -i -t -h sandbox sequenceiq/spark:1.2.0 /etc/bootstrap.sh -bash

    # -v Mount host /opt/rpm1 on image /opt/rpm1
    # -P map image ports to host port (see docker ps -l for mapping)
    docker run -v /opt/rpm1:/opt/rpm1 -P -i -t -h sandbox sequenceiq/spark:1.2.0 /etc/bootstrap.sh -bash

# Useful Docker Commands


    sudo docker ps -l  #Lists ports of running image (-a all images)
    sudo docker images #List docker images

