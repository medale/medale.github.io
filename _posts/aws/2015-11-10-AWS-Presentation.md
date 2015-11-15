---
layout: post
title: "Presentation: Amazon Web Services: Introduction, What's New & Java API"
description: "Presentation to the Baltimore Washington Java Meetup Group"
category: "aws"
tags: ["aws","aws-sdk","presentation","meetup"]
comments: true
---
In 2013 I took the excellent Coursera [Introduction To Data Science](https://www.coursera.org/course/datasci)
MOOC with Bill Howe from the University of Washington. Part of the class was
an optional assignment to use Amazon AWS Elastic MapReduce (EMR) to analyze
a dataset stored in Amazon S3 via Hadoop MapReduce. By taking the class, 
students qualified for a $100 educational credit from AWS to do this analysis.
That was my first exposure to doing big data in the cloud.

This year, I had a chance to take several AWS classes and use AWS more 
extensively. I also got to present at a panel at the
[Amazon AWS Re:Invent 2015 conference](https://reinvent.awsevents.com) and
had become a big fan of AWS.

**Steve O'Hearn**, the organizer of the 
[Baltimore Washington Java Meetup Group](http://www.meetup.com/dc-java/), 
invited me to speak about [Amazon AWS](http://aws.amazon.com) and the 
Re:Invent 2015 conference for the 
[Baltimore Washington Java Meetup on November 10th, 2015](http://www.meetup.com/dc-java/events/224396123/).
Despite rainy weather and horrible traffic we had a great and enthusiastic
turnout. Many thanks to Steve for organizing these meetups and pizza!
Our local AWS team also turned out to show their support and donated some door 
prizes. Many thanks also for their support! Excellent questions during the 
presentation were followed by lively discussions afterwards. **Many thanks for all the kind feedback!**

##Materials

* [Talk Slides](https://github.com/medale/presentations/blob/master/aws-overview-2015-10/AwsOverview.pdf)
* [Speaker Notes](https://github.com/medale/presentations/blob/master/aws-overview-2015-10/SpeakerNotes.pdf) provide some more in-depth descriptions.
* Sample code is available via:

{% highlight bash %}
git clone https://github.com/medale/presentations.git
cd presentations/aws-overview-2015-10/aws-sdk
mvn clean install

# See comments in S3Uploader on how to set up credentials and run main
{% endhighlight %}

