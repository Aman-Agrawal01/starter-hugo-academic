---
title: Quantum Query Complexity
subtitle: My first official blog! I have been learning query complexity and
  thought of writing it in a blog. This blog requires some basic understanding
  of quantum computing specifically the postulates of quantum mechanics.
date: 2020-12-13T00:00:00.000Z
summary: ""
draft: false
featured: false
authors: []
lastmod: 2020-12-13T00:00:00.000Z
tags: []
categories: []
projects: []
image:
  caption: ""
  focal_point: ""
  placement: 2
  preview_only: false
  filename: screenshot-2022-07-02-221551.png
---
Query Model
===

In Query Model, our task is to compute the function $f(x_1,x_2,....,x_n)$ by accessing $x_i$ through quering the orcale. Oracles can be thought of as a 'black-box' by which you can access some information regarding the input, we don't really care about the internal setup in black-box, it can be easily constructed. To access input, algorithm is allowed to query the oracle to get information on input. Hence, the aim of the algorithm is to take minimum queries to compute $f(x)$ on any input $x$. 

A quantum Oracle $O_x$ takes qubit $\lvert i \rangle$ where $i\in[n]$ in binary representation and $n\in \mathbb{N}$ and ancilia qubit $\lvert b \rangle$ and gives $\lvert i \rangle$ and $\lvert b \oplus x_i \rangle$ where $x_i$ is the $i^{th}$ bit of input $x$. 

$\begin{gather} O_x \lvert i \rangle \lvert b \rangle = \lvert i \rangle \lvert b \oplus x_i \rangle = (-1)^{b*x_i} \lvert i \rangle \lvert b \rangle\\ \end{gather}$

This type of oracle is known as bit-flip oracle. It's simply a unitary reversible mapping of $ (i,b) \mapsto (i, b \oplus x_i)$. Such type of mapping is used beacuse the operations we do in quantum computation should be unitary. An interesting fact, you can easily get back to $(i,b)$ from $(i,b \oplus x_i)$ by simply applying the same oracle $O_x$ to $(i,b \oplus x_i)$ due to the fact that $x_i \oplus x_i = 0$ for any $x_i$. 

I wanted to talk about one more oracle known as phase oracle which is widely used in quantum algorithms. You can take this as a special case of bit flip oracle where ancilia qubit is $\lvert - \rangle$ . The qubit $\lvert - \rangle$ is simply $\frac{\lvert 0 \rangle - \lvert 1 \rangle}{\sqrt{2}}$ . If we apply the bit flip oracle in this case, we can observe that the output would just changes the phase of our original state.

$\begin{gather} O_x \lvert i \rangle \lvert - \rangle = (-1)^{x_i} \lvert i \rangle \lvert - \rangle \\ \end{gather}$

Query Complexity
===

The query complexity is used in deterministic as well as quantum algorithms. One should note that there is a difference between query complexity of an algorithm and that of a function. 

The query complexity of an algorithm would be the minimum number of queries that it takes to compute the function $f(x)$ on any input $x$. 

The query complexity of a function is the minimum number of queries that an optimal algorithm takes in order to compute function $f(x)$ on any input $x$.

Why Query Model?
===

Now you might ask, why do we really need to know about query complexity? That's a valid question to ask. There are couple of reasons that convince us to have an idea about query complexity. 

Firstly, it's easy to analyse and a lot of known quantum algorithms like Shor's algorithm and Grover's search are based on query model. 

Secondly, it gives us a bound on time complexity of an algorithm. Finding the time complexity of a quantum algorithm is a tricky task but it turns out that if we are able to find the query complexity of the algorithm than we know that time complexity is larger than query complexity and hence gets some idea about the time complexity of an algorithm.

Conclusion 
===

So, that's it! Hope you like the blog :) I am planning to write one more blog on a result "the approximate degree gives a lower bound on quantum query complexity". 