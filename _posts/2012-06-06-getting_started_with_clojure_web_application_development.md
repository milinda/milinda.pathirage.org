---
layout: post
title: Web Application Development in Clojure
author: Milinda Pathirage
date: 2012-06-06 18:54:11
comments: true
---

I did some coding in [Scheme](http://en.wikipedia.org/wiki/Scheme_(programming_language)) and [Ruby](http://www.ruby-lang.org/en/) last couple of months and felt that writing Java code is not fun anymore. But Java as a platform is really good for
most of the tasks and I started to learn some [Clojure](http://clojure.org/) because there is support for reusing Java libraries in Clojure and it's a really good mordern [Lisp](http://en.wikipedia.org/wiki/Lisp_(programming_language) derivative.

I'm new to Clojure and I found the series of [blog posts](http://writingcoding.blogspot.com/2008/06/clojure-series-table-of-contents.html) by Eric Rochester is really helpful to understand basic stuff for a beginner like me. Please keep in mind that there are some incompatibilities in the code of above blog posts with the new Clojure versions.

As a start I started to re-wrtie a partially done Java Web Service in
Clojure as a REST service. So I googled for resources on Clojure web
appliction development and found [this tutorial](http://mmcgrana.github.com/2010/07/develop-deploy-clojure-web-applications.html). That is really good tutorial for beginners and it covers most of the basic concepts of [Ring](https://github.com/mmcgrana/ring), [Compojure](https://github.com/weavejester/compojure) and [Hiccup](https://github.com/weavejester/hiccup). But there were some small issues and most of the solitions can be found in the comments section. My code for above tutorial can be found [here](https://github.com/milinda/ef/tree/master/clojure-web/adder).

There are slight changes in my code when compared to code in the
tutorial.

* I didn't create a separate *script/run.clj* file, but included main
  method in *adder/core.clj*.
* Had to modify *form action* and *link* in output view to make this
  work as a WAR in Tomcat.
* Used [lein](https://github.com/technomancy/leiningen)-[ring](https://github.com/weavejester/lein-ring) to create WAR file and had to exclude *javax.servlet* jar from the generated WAR file using *:war-exclusions* to resolve a class loading issue.
* I had to serve static files via Tomcat because ring middleware
  'wrap-file' couldn't load my resource directory when I bundled the app
as a war. So I used *:war-resources-path* configuration to copy
resources(static files) into root of my WAR.

I learned several things by doing this excercise. One thing is support
for WAR deployment is still in early stage. Mostly it's hard to find
good resources online. And the other thing is some of the most popular
tutorials available online are outdated. This is mainly due to rapid
changes(development) in Clojure eco-system. Finally there are some stuff
which works with Jetty adapter doesn't work when deploy the WAR in a
custom context and I couldn't find any tutorial which talks about these
things. I think *wrap-if* concept introduced in Clojure web app development [tutorial]((http://mmcgrana.github.com/2010/07/develop-deploy-clojure-web-applications.html) I mentioned above will be really helpful to handle development and production configurations.

IMO, If you are new to web application development in Clojure following
resources will be really helpful to you.

* [Developing and Deploying a Simple Clojure Web Application](http://mmcgrana.github.com/2010/07/develop-deploy-clojure-web-applications.html)
* [Building REST APIs for Clojure Web Applications](http://mmcgrana.github.com/2010/08/clojure-rest-api.html)
* [A Brief Overview of the Clojure Web Stack](http://brehaut.net/blog/2011/ring_introduction)
* [Noir](http://webnoir.org/)

If you are thinking of developing web applications in Java, consider
moving to Clojure. It's really fun than developing in Java ;-).
