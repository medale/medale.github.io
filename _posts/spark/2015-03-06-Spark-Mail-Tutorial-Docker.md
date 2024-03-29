---
layout: post
title: "Spark Mail Tutorial On Docker"
description: "How to run the Spark Mail Tutorial on Docker"
category: "spark"
tags: ["spark","docker", "tutorial"]
---

See [medale spark-mail-docker github repo](https://github.com/medale/spark-mail-docker)

# Installing Docker

* [Docker Installations](https://docs.docker.com/installation/)

# Obtaining medale/spark-mail-docker from DockerHub


    sudo docker pull medale/spark-mail-docker:v1.2.1


# Run spark-mail-docker image

## Simple run (no shared drive)

* -P map image ports to host port (see docker ps -l for mapping)
* -i run in interactive mode
* -t with tty terminal
* -h sets hostname of the image to "sandbox"
* medale/spark-mail-docker:v1.2.1 image and version of image
* /etc/bootstrap.sh - complete bootstrap
* bash - then run bash (login as root)



    sudo docker run -P -i -t -h sandbox medale/spark-mail-docker:v1.2.1 /etc/bootstrap.sh bash


## Mounting a share drive to the image

-v Mount host /opt/rpm1 on image /opt/rpm1 (share files between image and host)


    sudo docker run -v /opt/rpm1:/opt/rpm1 -P -i -t -h sandbox medale/spark-mail-docker:v1.2.1 /etc/bootstrap.sh bash
    > Starting sshd:                                             [  OK  ]
    > Starting namenodes on [sandbox]
    > sandbox: starting namenode, logging to /usr/local/hadoop/logs/hadoop-root-namenode-sandbox.out
    > localhost: starting datanode, logging to /usr/local/hadoop/logs/hadoop-root-datanode-sandbox.out

# Image layout
Running the image with the bash command brings you to a shell prompt as root:


    pwd
    > /root
    ls
    > enron-small.avro  log4j.properties  mailrecord-utils-0.9.0-SNAPSHOT-shaded.jar	start-spark.sh
    hdfs dfs -ls
    > Found 2 items
    > -rw-r--r--   1 root supergroup  324088129 2015-03-01 22:11 enron.avro
    > drwxr-xr-x   - root supergroup          0 2015-01-15 04:05 input
    env
    > SPARK_HOME=/usr/local/spark
    > JAVA_HOME=/usr/java/default
    > YARN_CONF_DIR=/usr/local/hadoop/etc/hadoop
    > ...

# Running Spark with minimum logging and kryo serialization


    (if you are not in /root, cd /root)
    ./start-spark.sh
    > Spark assembly has been built with Hive, including Datanucleus jars on classpath
    > ...
    > scala>


# Analytic 1

{% highlight scala %}
    scala>:paste
    import org.apache.spark.SparkContext._
    import org.apache.spark.rdd._
    import com.uebercomputing.mailparser.enronfiles.AvroMessageProcessor
    import com.uebercomputing.mailrecord._
    import com.uebercomputing.mailrecord.Implicits.mailRecordToMailRecordOps
    val args = Array("--avroMailInput", "enron.avro")
    val config = CommandLineOptionsParser.getConfigOpt(args).get
    val recordsRdd = MailRecordAnalytic.getMailRecordsRdd(sc, config)
    recordsRdd.cache
    val d = recordsRdd.filter(record => record.getFrom == "dortha.gray@enron.com")
    d.count
    > resN: Long = 8
{% endhighlight %}

# Accessing Spark Web UI

Docker creates an internal IP address for the image we started. To determine
this IP address we can either do this from the host machine:

```
sudo docker ps
> CONTAINER ID        IMAGE                      COMMAND                CREATED             STATUS              PORTS
> bb5cf832bd76        medale/spark-mail-docker:v1.2.1   "/etc/bootstrap.sh /   13 minutes ago      Up 13 minutes       0.0.0
sudo docker inspect --format=".NetworkSettings.IPAddress" bb5cf832bd76
> 172.17.0.71
```

Or we could run the following on the image container:

```
ifconfig
> eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:12  
           inet addr:172.17.0.71  Bcast:0.0.0.0  Mask:255.255.0.0
...
```

Now we can go to the Resource Manager from local browser on host:
* http://172.17.0.71:8088/

From there, click on ApplicationMaster (under TrackingUI column). The link goes
to something like:

* http://sandbox:8088/proxy/application_1425314491113_0001/ (which does not exist)
* Replace sandbox with the previously obtained IP address, for example:
* http://172.17.0.71:8088/proxy/application_1425314491113_0001/


## Creating a host alias to avoid having to replace "sandbox"

Alternatively, on Linux, we can use the HOSTALIASES environment variable to
temporarily map sandbox to the container IP address and then run our browser
with that environment variable to translate sandbox references to the container IP:

On your host, edit host-alias with the container IP address.
For example this host-alias:


    sandbox 172.17.0.71


Then:


    export HOSTALIASES=host-alias
    # start firefox in background with that environment variable set
    firefox


In the browser, go to http://sandbox:8088/. Now all http://sandbox... links
on that page should work.

# Image Overview

In addition to Hadoop we have:

## Customized spark-1.2.1

We then add a customized spark-1.2.1.tar.gz. See [these
instructions](https://github.com/medale/spark-mail/blob/master/presentation/CreatingAvroMapred2Spark.md)
on how to build this distro (tar assumes directory spark-1.2.1-hadoop2.4 inside of the tar.gz file).

## Other files not in this github repo

* enron-small.avro - an arbitrary subset (however big you want to process) of Avro version of Enron emails.
See [Spark Mail README.md](https://github.com/medale/spark-mail/blob/master/README.md) for overview of how to
obtain the emails and convert them to .avro format. Also see [Main.scala](https://github.com/medale/spark-mail/blob/master/mailrecord-utils/src/main/scala/com/uebercomputing/mailparser/enronfiles/Main.scala).

## Additional files

* log4j.properties - suppresses DEBUG and INFO messages for less clutter
* start-spark.sh - script to start up Spark shell in yarn-client mode with Kryo

# Building medale/spark-mail-docker locally

* must create spark-1.2.1.tar.gz (see above)
* must create enron-small.avro (see above)

Add both files to docker-spark directory (same directory as Dockerfile).


    sudo docker build -t medale/spark-mail-docker .
    sudo docker images  #lists container id (assumed here to be e57ff7c77397)
    sudo docker tag e57ff7c77397 medale/spark-mail-docker:v1.2.1

# (Optional) Publish to DockerHub

After creating account on [DockerHub](https://hub.docker.com/account/signup/)
you can publish your image to a public repo so others can find and pull it
without having to build the image locally:


    sudo docker push medale/spark-mail-docker:v1.2.1
    sudo docker search medale
    sudo docker pull medale/spark-mail-docker:v1.2.1


# Other useful Docker commands

```
    # Show available images
    sudo docker images
    > REPOSITORY                 TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    > medale/spark-mail-docker          v1.2.1              5e4665af6d6e        13 hours ago        2.84 GB
    > ...

    # Delete a local image
    sudo docker rmi training/sinatra

    # Delete a stopped instance
    sudo docker ps -a -q # show all containers, just id
    sudo docker rm <container id>

    # Show docker container ids
    sudo docker ps -l

    # Commit changes to an image
    sudo docker commit <container_id> medale/new_image
```

For background see [dockerimages](https://docs.docker.com/userguide/dockerimages/)
and [Docker builder reference](https://docs.docker.com/reference/builder/).

# Dockerfiles lore

ADD local.jar /some-container-location
If src is a local tar archive in a recognized compression format (identity, gzip, bzip2 or xz) then it is unpacked as a directory
