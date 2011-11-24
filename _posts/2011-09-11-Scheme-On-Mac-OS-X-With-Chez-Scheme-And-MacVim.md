---
layout: post
title: Scheme on Mac OS X With Chez Scheme And MacVim
author: Milinda Pathirage
time: 11th September 2011 
comments: true
---

When I began using Scheme, I used Emacs with free version of [Chez Scheme](http://www.scheme.com/). I had little experience with Emacs and I had to learn required key-board shortcuts as well as I had to customize Emacs with .emacs file to make Emacs scheme mode work with Petite interpreter. The process was harder and programming Scheme was also harder because I am not that familiar with Emacs.

<img src="/images/mavim-scheme.png"/>

I found a nice [blog post](http://jeffkreeftmeijer.com/2011/vim-is-hard-i-just-want-to-click-around/) about [MacVim](http://code.google.com/p/macvim/) a week earlier and I gave it a try. I compiled [@alloy](http://twitter.com/alloy)'s MacVim [fork](https://github.com/alloy/macvim) with Ruby and Python enabled. And also installed [Janus](https://github.com/carlhuda/janus) Vim configuration by [@wycats](http://twitter.com/wycats) and [@carllerche](http://twitter.com/carllerche), which comes with awesome set of plugins and color themes. When customized with my own personal settings this new Vim configuration is the best Vim configuration I ever had.

Janus Vim config install [Conque](http://code.google.com/p/conque/) Vim plugin which allows you to run interactive programs inside Vim buffer. This became handy when testing Scheme code I am writing while inside the editor. All you have to do is split your Vim window vertically and run *bash* inside new split section using Conque. You just need to execute **:ConqueTermSplit bash** and once the bash is running you can run *petite* interpreter inside that.

Make sure to download **Petite Chez Scheme** non-threaded Mac OS X [pkg file](http://www.scheme.com/download/pcsv8.3-a6osx-2.pkg.tar.gz) suitable to your architecture. When compiling MacVim make sure to enable Python and Ruby support. You can do this by running configuration script as follows: **./configure --enable-rubyinterp=yes --enable-pythoninterp=yes**.