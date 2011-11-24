---
layout: post
title: Mutual Recursion
author: Milinda Pathirage
time: 3rd September 2011
comments: true
---

While doing the [Programming Language](https://www.cs.indiana.edu/cgi-pub/c311/doku.php) course assignment I came across following question:

*Define and test two **mutually recursive** procedures even-layers? and odd-layers? that take an *onion* of the form (((…))). The even-layers? procedure should return #t if the onion has an even number of layers and #f otherwise, and odd-layers? should return #t if the onion has an odd number of layers and #f otherwise. The onion () has zero layers.*

To be frank, I didn't know anything about mutual recursion. There is a possibility that I had heard about it before, but nothing came into my mind when I saw the question. So I googled and found the [Wikipedia page](http://en.wikipedia.org/wiki/Mutual_recursion) for mutual recursion. Example in that Wikipedia page helped me to understand what mutual recursion is in couple of seconds.

Here is the solution to the above problem in Scheme:

<script src="https://gist.github.com/1192201.js"> </script>
