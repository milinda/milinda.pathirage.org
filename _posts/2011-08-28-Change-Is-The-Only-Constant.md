---
layout: post
title: Change Is The Only Constant
author: Milinda Pathirage
time: 28th August 2011 
comments: true
---

I am a guy who liked to change the design of my blog time to time. I use [Wordpress](http://wordpress.org/) as the blogging platform for [blog.mpathirage.com](http://blog.mpathirage.com) and I am using Wordpress from June 2008. But the main problem I had was the complexity of Wordpress platform. It's very hard to change the look and feel and site structure without going through the complexity of Wordpress themes and plugins. 

In addition to that I didn't use any of the advance features of Wordpress(my blog is pretty simple one with couple of posts per month) and given the performance overhead and complexity it was not worth maintaining it. If I remember correctly I got to know about [Jekyll](https://github.com/mojombo/jekyll) about a year ago. But couldn't migrate my blog to [Jekyll](https://github.com/mojombo/jekyll) due to time constraints.

I moved to [Bloomington](http://bloomington.in.gov/), Indiana to do my PhD in computer science this August(2011) and I had plenty of time to play with [Jekyll](https://github.com/mojombo/jekyll) during the orientation period. And I found out about the [Amazon S3](http://aws.amazon.com/s3/) [static web site hosting feature](http://aws.amazon.com/about-aws/whats-new/2011/02/17/Amazon-S3-Website-Features/) and decided to host the blog in Amazon S3. 

So this new blog is the result of work I did around [Jekyll](https://github.com/mojombo/jekyll) and Amazon S3. [Jekyll](https://github.com/mojombo/jekyll)'s theming system and configurations are pretty easy and I could write my own theme using [Jekyll-Base](https://github.com/danielmcgraw/Jekyll-Base) as the foundation within couple of hours. I'm using [Dropbox](http://www.dropbox.com/) to keep a backup of the site's source and use [s3sync](https://forums.aws.amazon.com/thread.jspa?threadID=11975&start=0&tstart=0) written in Ruby to sync the new site to S3 bucket.

Here are some helpful links to get started with Jekyll and Amazon S3 website hosting.

 - [Ultimate guide to getting started with Jekyll](http://danielmcgraw.com/2011/04/14/The-Ultimate-Guide-To-Getting-Started-With-Jekyll-Part-1/)
 - [Host your static web site on Amazon S3](http://aws.typepad.com/aws/2011/02/host-your-static-website-on-amazon-s3.html)
 - [Hosting Websites on Amazon S3](http://docs.amazonwebservices.com/AmazonS3/latest/dev/index.html?WebsiteHosting.html)
 - [How to alias domain name or sub domain name to Amazon S3](http://carltonbale.com/how-to-alias-a-domain-name-or-sub-domain-to-amazon-s3)
 
So in the coming years I'll use this site as the my primary blog and I am planning to migrate some of the popular posts from my old [blog](http://blog.mpathirage.com) to this one. May be this blog will also change in the future. Who knows what will happen in the future. Change is the only constant.


> Everyone thinks of changing the world, but no one thinks of changing himself.