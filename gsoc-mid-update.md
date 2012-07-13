---
layout: layout
title: GSOC 2012 Midterm Update
---

<h1>GSOC 2012 Midterm Update</h1>

This is a brief summary of work I did from May 21st to July 11th. I started by 
porting GFac [Hadoop](http://hadoop.apache.org/) provider from [OGCE](http://sourceforge.net/projects/ogce/)
to Airavata [GFac](http://incubator.apache.org/airavata/documentation/gfac/gfac.html). That version of Hadoop provider only had support for
already configured Hadoop deployment. After that I did some experiments
with Apache [Whirr](http://whirr.apache.org/) based Hadoop deployment(EC2) and integrated Apache
Whirr to GFac Hadoop provider. This enables GFac to automatically deploy
Hadoop cluster in EC2 or in local cluster and execute jobs in the
deployed cluster.

After implementing Hadoop deployment and job execution support I had to
decide on how to handle data movement in/out to/from HDFS. After
discussing with my mentor we came up with following solutions:

* Implement the input/output data staging outside the GFac and provide them as XBaya workflow activities. So that the users who are using Hadoop support in XBaya can handle data staging on their own. 
*  Implement data staging support inside GFac. Based on the input data location and output data location specified by the user GFac will automatically handle the data movement before/after Hadoop job execution.

We presented these solutions to Airavata team in a off line discussion
and their preference was to go ahead with the second approach. While
studying GFac for implementing data movement support I found out that
most of the current data movement logics are implemented in ad-hoc
manner for currently supported GFac providers. Even though GFac
architecture is built on top of *'Chain of Responsibility'* pattern, I
found out that current implementation doesn't correctly use that. So
after discussing with my mentors I decided to deviate from the plan I
proposed in the initial [GSOC proposal](http://milinda.pathirage.org/gsoc.html) 
and refactor GFac to suits to our requirements and initial GFac
architecture. Currently I am working on the refactorings and source can
be found [here](http://svn.codespot.com/a/apache-extras.org/airavata-gsoc-sandbox/trunk/milinda).

<h2>Updated project plan</h2>

<h3>Phase 1</h3>

Same as in the [original proposal](http://milinda.pathirage.org/gsoc.html).

<h3>Phase 2</h3>
[GFac refactorings](https://issues.apache.org/jira/browse/AIRAVATA-477) and implement data movement support in/out to/from
HDFS.

<h3>Phase 3</h3>
Improvements to GFac scheduler and Cloud bursting support as discussed
in [original proposal](http://milinda.pathirage.org/gsoc.html) under
**Phase 2**.

<h2>Progress up to midterm</h2>
* **Phase 1(completed)** - Implemented Hadoop provider using Apache
  Whirr for cloud and local cluster deployment. Code can be found in the
original [issue](https://issues.apache.org/jira/browse/AIRAVATA-357) as
a patch.
* **Phase 2(in-progress)** - Currently working on refactoring GFac. Code
  can be found [here](http://svn.codespot.com/a/apache-extras.org/airavata-gsoc-sandbox/trunk/milinda) in Apache Extras.


