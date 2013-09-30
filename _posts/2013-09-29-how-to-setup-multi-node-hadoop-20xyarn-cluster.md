---
layout: post
title: "How To Setup Multi Node Hadoop 2.0.x(YARN) Cluster"
date:   2013-09-29
author: Milinda Pathirage
categories: hadoop yarn
excerpt: There are lots of online articles on installing Hadoop. But not many on Hadoop YARN. But the articles I found didn't work for Hadoop 2.0.6. I had to read the Hadoop code and figure out the issues. This post descibres proper and easy way to install Hadoop 2.0.6-alpha(YARN) on a 2-node cluster.
---

This post describes neccessary steps required to setup 2-node [Hadoop YARN](http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html) cluster using Hadoop [2.0.6-alpha](http://hadoop.apache.org/docs/r2.0.6-alpha/) release. This post is based on \[[1](#references)\] and \[[2](#references)\] and can be considered as a combination of both posts with extra steps necessary to setup Hadoop 2.0.6-alpha. Steps I discussed here should also work for Hadoop [2.1.0-beta](http://hadoop.apache.org/docs/r2.1.0-beta/). 

## 1. User accounts, /etc/hosts file modifications and password less SSH

You can follow the steps described in \[[1](#references)\] under section "**User creation and other configurations steps**" to setup necessary user accounts and password less SSH. One thing to make sure that password less ssh for locahost, in addition to slaves. \[[2](#references)\] doesn't mention about password less SSH for **localhost**, but it is important. Otherwise startup scripts will ask you to type the password during *data node* and *node manager* startup.

## 2. Configuring Hadoop

You can follow the steps 4, 5, 6, 7, and 8 described in \[[2](#references)\] to configure Hadoop with some small modifications noted below.

* During step 5 in \[[2](#references)\], you need to add **JAVA_HOME** environment variable to *hadoop-env.sh* too.
* One of the most important configuration step is configuring *yarn.nodemanager.address* and *yarn.nodemanager.localizer.address* in *yarn-site.xml* during step 7 discussed in \[[2](#references)\]. We need this configuration change only in master node due to the fact that both resource manager and node manager will run on master node and if we don't have a node manager address and localizer address specific to node manager, node manager will try to bind to same ports which uses by resource manager. 

So with above mentioned change yarn-site.xml will look like following after necessary changes.

{% highlight xml %}
<?xml version="1.0"?>
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce.shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
  <property>
    <name>yarn.resourcemanager.resource-tracker.address</name>
    <value>master:8025</value>
  </property>
  <property>
    <name>yarn.resourcemanager.scheduler.address</name>
    <value>master:8030</value>
  </property>
  <property>
    <name>yarn.resourcemanager.address</name>
    <value>master:8040</value>
  </property>
  <property>
    <name>yarn.nodemanager.address</name>
    <value>master:8050</value>
  </property>
    <property>
    <name>yarn.nodemanager.localizer.address</name>
    <value>master:8060</value>
  </property>
</configuration>
{% endhighlight %}

## 3. Running Hadoop YARN and Checking Installation

You can follow steps 9, 10, 11 and 12 in \[[2](#references)\] to start and test the installation. You can find necessary information about web interface URLs and how to stop Hadoop YARN cluster in last part of \[[2](#references)\].


<div class="references" id="references"> 
     <h2>References</h2>
<p>[<a href="http://www.javacodegeeks.com/2013/06/setting-up-apache-hadoop-multi-node-cluster.html" target="_blank">1</a>]. Piyas De, <strong><em>Setting up Apache Hadoop Multi – Node Cluster</em></strong></p>
<p>[<a href="http://raseshmori.wordpress.com/2012/10/14/install-hadoop-nextgen-yarn-multi-node-cluster/" target="_blank">2</a>]. Rasesh Mori,  <strong><em>Steps to install Hadoop 2.x release (Yarn or Next-Gen) on multi-node cluster</em> </strong></p>
</div>

