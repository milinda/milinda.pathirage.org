---
layout: post
title: LLVM Based Scheme Compiler In Ruby(Part 1)
author: Milinda Pathirage
date: 2012-05-19  0:06:53
---
<div class="alert alert-info">
<p style="margin-bottom: 2px;">I am not a programming language expert and doing this as a exercise to learn more about programming language implementations, so there can be errors in things I am saying. Please feel free to comment on the post if you find anything incorrect.</p>
</div>
I wanted to do a implementation of a known language since I did [Programming Language Principles](https://www.cs.indiana.edu/cgi-pub/c311/doku.php) course in fall 2011. To learn more about programming language implementation I did the [Programming Language Implementaiton](https://www.cs.indiana.edu/~achauhan/Teaching/P523/2012-Spring/index.html) course in spring 2012. I learned lot of new things from those courses including functional programming, continuations, interpretation, code generation, compiler optimizations and etc. Finally I got some free time this summer and started this project, implementing [Scheme](http://en.wikipedia.org/wiki/Scheme_(programming_language\)) to [LLVM](http://llvm.org/) [Assembly](http://llvm.org/docs/LangRef.html) compiler.

This is the first post of series of posts I'm planning to write on compiling Scheme to LLVM IR(aka LLVM assembly). Rest of the post will discuss reasons for choosing Scheme, good resources for learning about techniques I am going to use in this project and [Treetop](http://treetop.rubyforge.org/) based parser for Scheme.

#### Why Scheme?

I implemented a C(small subset) to LLVM IR compiler as a assignment of
Programming Language Implementation course. But for this project I
choose Scheme because it's heavy use in academia, Scheme is a good
language for learning programming language concepts and compiling
Scheme involves fun things like closure conversion, tail-call handling,
first-class continuation handling and automatic memory management.

I am using LLVM because I have some previous experience using it and it's modular architecture allows us to experiment with different optimizations and wirte our own optimization easily if needed. Ruby is choosen mainly because of [ruby-llvm](https://github.com/jvoorhis/ruby-llvm). [Treetop](http://treetop.rubyforge.org/) will be used as the parser generation framework.

#### Reading List

I found following blogs and books are pretty helpful to learn about programming language implementation.

* <a href="http://www.amazon.com/gp/product/0521545668/ref=as_li_qf_sp_asin_tl?ie=UTF8&tag=thinksquared-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0521545668">Lisp in Small Pieces</a><img src="http://www.assoc-amazon.com/e/ir?t=thinksquared-20&l=as2&o=1&a=0521545668" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" /> is great book for learning programming language implementation techniques and Scheme to C compilation.
* [7 lines of code, 3 minutes: Implement a programming language from scratch](http://matt.might.net/articles/implementing-a-programming-language/)
* [Writing a language in 15 minutes](http://blog.jcoglan.com/2009/05/19/talk-writing-a-language-in-15-minutes/)
* [A quick intro to writing a parser with Treetop](http://thingsaaronmade.com/blog/a-quick-intro-to-writing-a-parser-using-treetop.html)
* [Treetop presentaiton](http://www.slideshare.net/eventRT/tree-top-5608926)


### More Resources
* [kid-scheme](http://code.google.com/p/kid-scheme/)
* [LLVM Tutorial](http://llvm.org/docs/tutorial/)
