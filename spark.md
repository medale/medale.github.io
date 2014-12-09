---
layout: page
title: Spark Nuggets
tagline: Continuous improvement through project, practices, self
---
{% include JB/setup %}

# REPL

* [Log4J logging setup for Spark](http://stackoverflow.com/questions/25193488/how-to-turn-off-info-logging-in-pyspark)

Print full classpath used to launch shell:
     
    SPARK_PRINT_LAUNCH_COMMAND=1 bin/spark-shell

Scala REPL show defined terms
   
    $intp.definedTerms.foreach(println)

Enter paste mode

    :paste
    
# Misc

## User classpath
    spark.yarn.user.classpath.first
    spark.files.userClassPathFirst=true
    
## Building Spark via Maven

    export MAVEN_OPTS="-Xmx2g -XX:MaxPermSize=512M -XX:ReservedCodeCacheSize=512m"
    mvn -Pyarn -Phadoop-2.4 -Dhadoop.version=2.4.0 -DskipTests clean package

## Scala - rename import

    import org.apache.spark.mllib.linalg.{Vector => SparkVector}


# Code Snippets

{% highlight scala %}
 val recordsKeyValues = sc.newAPIHadoopRDD(conf.getConfiguration,
        classOf[AvroKeyInputFormat[MailRecord]],
        classOf[AvroKey[MailRecord]],
        classOf[NullWritable])
{% endhighlight %}

