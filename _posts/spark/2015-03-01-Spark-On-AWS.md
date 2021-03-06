---
layout: post
title: "Spark On AWS"
description: "Running Spark on AWS"
category: "spark"
tags: ["spark","aws", "emr"]
---

# Spark Demo on AWS

Recently, I had the pleasure of working with [JT Halbert](https://github.com/jt-halbert)
and [Jason Morris](https://github.com/notjasonmorris/) on creating
an AWS-based Spark demo using the Enron email dataset for the 
[Apache Spark Maryland meetup](http://www.meetup.com/Apache-Spark-Maryland/).

I had worked on putting together a Spark demo for the Enron email dataset
and provided all the ETL to put the text-based CMU Enron email set into Avro
along with some utilties to make it easy to explore from spark-shell.

As part of this, I also wanted to try out my code on the AWS cluster but did 
not know how much it would cost to run. Estimates were available at
on [Amazon's EMR pricing](http://aws.amazon.com/elasticmapreduce/pricing/), which
seemed very reasonable. Instance types were described on the [EC2 instance types page](http://aws.amazon.com/ec2/instance-types/).
So I decided to just try it out.

First, I installed the AWS CLI following the [Amazon CLI instructions](http://aws.amazon.com/cli/)
with Python 2.6.5 or higher:


    sudo apt-get install python-pip
    sudo pip install awscli


I then used [Jason's demo.sh](https://github.com/notjasonmorris/AWS/blob/master/EMR/demo.sh)
to spin up a three-node cluster with a custom 1.2.1 Spark on m3.xlarge instances. Note:
demo.sh also downloads some datasets, which you may or may not want. Modify to
suit your needs.

I ran for 232 minutes (not realizing that usage is charged by the hour so I
could have run for 300 minutes for the same cost - 120 normalized instance
hours). The total cost for this was $5.55 broken out as:

* $0.30 in data transfer
* $4.20 EC2
* $1.05 EMR
* 232 minutes (always charged by fraction of full hours)
* 120 normalized instance hours
* Instance type: m3.xlarge

This data was gathered from:
* [AWS Console Billing - Bills](https://console.aws.amazon.com/billing/) - actual costs
* [AWS Console EMR](https://console.aws.amazon.com/elasticmapreduce) - actual runtime/size of clusters

# EMR AMI versions

The key line in the demo.sh script for cluster creation is:

     aws emr create-cluster --name SparkCluster --ami-version 3.2 --instance-type m3.xlarge --instance-count 3  --ec2-attributes KeyName=$KEYNAME


The ami-version for EMR determines what Hadoop ecosystem is on the box.
See [AMI for EMR overview](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/ami-versions-supported.html).
So we were running on Hadoop 2.4.0.

Bottom line: AWS EMR and CLI are great utilities to launch a Spark cluster
on demand!

# Background on AWS setup
* Create [IAM user](https://console.aws.amazon.com/iam) for access keys

Enter access key id, secret access key when prompted or create aws-env.sh and
source that before running the demo.sh script:

    export AWS_ACCESS_KEY_ID=keyId
    export AWS_SECRET_ACCESS_KEY=secretAccessKey (longer than key id)
    export AWS_DEFAULT_REGION=us-east-1
    
 
