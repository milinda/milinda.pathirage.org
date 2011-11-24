---
layout: post
title: Wrap The Natural Recursion
author: Milinda Pathirage
time: 28th August 2011 
comments: true
---

Today(30th August 2011) is the first day of my "[Programming Language Principles](https://www.cs.indiana.edu/cgi-pub/c311/doku.php)" class taught by Professor [Daniel Friedman](https://www.cs.indiana.edu/~dfried/). To be frank, it was the best lecture I have ever been to(Its look like upcoming lectures will be more interesting than today's one). I'm going to introduce you to the some of the concepts I learned today. We use Scheme as our medium for learning the general concepts in programming languages.

### Two kinds of Data Structures 
In this [course](https://www.cs.indiana.edu/cgi-pub/c311/doku.php) we are mainly interested in two kinds of data structures.

* Atoms - Any data construct that is a single value (symbols, numbers, strings, and boolean values)
* Lists - (S<sub>1</sub> S<sub>2</sub> ..... S<sub>k</sub>) where S<sub>i</sub> can be a **Atom** or **List**.

### Five fundamental building blocks
As I understood we are going to use following five building blocks in our future programs and exercises. There are lot of in-built functions in Scheme, but we can solve lot of problems using these fundamental building blocks. 

Contents of the below 'list' are (S<sub>1</sub> S<sub>2</sub> ..... S<sub>k</sub>).

* (**car** list) = S<sub>1</sub>; If argument given is not a list program will fail.
* (**cdr** list) = (S<sub>2</sub> ..... S<sub>k</sub>);If argument given is not a list program will fail.
* (**cons** S<sub>0</sub> list) = (S<sub>0</sub> S<sub>1</sub> S<sub>2</sub> ..... S<sub>k</sub>) 
* (**eq?** A<sub>1</sub> A<sub>2</sub>) = #t if two atoms are identical #f otherwise
* (**atom?** S) = #t if S is an atom #f otherwise

**car** returns the first element of the list, and **cdr** returns the remainder. Procedure **cons** construct lists by taking two arguments. Most of the times second argument will be a list, in that case **cons** returns a list. Procedure **cons** actually build pairs, for more information refer [Section 2.2. Simple Expressions](http://www.scheme.com/tspl4/start.html#./start:h2) of [The Scheme Programming Language](http://www.scheme.com/tspl4/).

So now we know some of the fundamental building blocks that we can used to implement solutions to simple computing problems. Let's start by implementing procedure **null?**, which takes one argument and determines whether its operand is a empty list, returning *True* if it is and *False* otherwise.

<script src="https://gist.github.com/1183529.js"> </script>

Above example contains a new procedure called **cond** which I haven't explain above. **cond** is similar to **if**, but it allows multiple tests and alternative expressions.

Last part of the lecture was on **Recursion**. 

### Recursion
I found some old Programming Language [course notes](http://www.cs.indiana.edu/eip/script2), and it says **Recursion** is an application of mathematical induction to programming. [This](http://lambda-the-ultimate.org/node/997) thread from [Lambda the Ultimate](http://lambda-the-ultimate.org/) contains some nice discussions around recursion and iteration based programming. Most of the arguments are related to above definition which says **Recursion** is coming from mathematical world.

So let's look at couple of examples described under recursion.

#### Union of two sets
The union of two sets A <span>&cup;</span> B is defined as { x | x <span>&isin;</span> A <span>&or;</span> x <span>&isin;</span> B}.

If you refer to [course notes](http://www.cs.indiana.edu/eip/script2) I mentioned above, you can find the steps in defining a recursive procedure in the last part of that document. I'll list down the main steps from the above document and please refer to it for more details.

0. State you GOAL.
1. Determine the BASE CASE(S).
2. Write the NATURAL RECURSION.
3. Determine the COMPLETION.
4. Express the goal in terms of the completion and natural recursion.

So let's apply the above to implement a recursive procedure for union of two sets.

0. We come up with the following skeleton for our solution.
	<script src="https://gist.github.com/1184327.js"> </script>
1. The simplest case is when **firstSet** becomes **null**. When first set is null we can return **secondTest** as the result. So we test for this BASE CASE with **(null? firstSet)**.
	<script src="https://gist.github.com/1184352.js"> </script>
2. Now if **firstSet** is not empty, if the first element of **firstSet** is in the **secondSet** we prepare for the recursion by noting that we can simplify the **firstSet** with **cdr**.
	<script src="https://gist.github.com/1184396.js"> </script>
	(union (cdr firstSet) secondSet) is called NATURAL RECURSION.
3. If the first item of the **firstSet** is not a member of **secondSet**, we must **cons** the **(car firstSet)** with the NATURAL RECURSION to get the COMPLETION.
	<script src="https://gist.github.com/1184414.js"> </script>
4. Finally we can express the our goal in terms of natural recursion and the completion. 
	<script src="https://gist.github.com/1184422.js"> </script>

The above problem is bit complex because we have two places where we apply natural recursion. To understand more on wrapping natural recursion I strongly recommend you to read [course notes](http://www.cs.indiana.edu/eip/script2) I mentioned above. Those notes will help you to understand how to apply natural recursion to solve real world computing problems. Also read [The Scheme Programming Language](http://www.scheme.com/tspl4/) if you want to learn more on Scheme. 





>"If you don't understand interpreters, you can still write programs; you can even be a comptent programmer. But you can't be a master" ~ Hal Abelson


  