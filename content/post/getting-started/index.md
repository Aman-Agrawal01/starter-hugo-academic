---
title: Quantum Query Complexity
subtitle: My first official blog! I have been learning query complexity and
  thought of writing it in a blog. This blog requires some basic understanding
  of quantum computing specifically the postulates of quantum mechanics.
date: 2020-12-13T00:00:00Z
summary: Welcome 👋 We know that first impressions are important, so we've
  populated your new site with some initial content to help you get familiar
  with everything in no time.
draft: false
featured: false
authors:
  - admin
  - 吳恩達
lastmod: 2020-12-13T00:00:00Z
tags:
  - Academic
  - 开源
categories:
  - Demo
  - 教程
projects: []
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false
---
<!--StartFragment-->

# Query Model[](https://aman-agrawal01.github.io/posts/2021/11/query_complexity/#query-model "Permalink")

In Query Model, our task is to compute the function f(x1,x2,….,xn) by accessing xi through quering the orcale. Oracles can be thought of as a ‘black-box’ by which you can access some information regarding the input, we don’t really care about the internal setup in black-box, it can be easily constructed. To access input, algorithm is allowed to query the oracle to get information on input. Hence, the aim of the algorithm is to take minimum queries to compute f(x) on any input x.

A quantum Oracle Ox takes qubit |i⟩ where i∈\[n] in binary representation and n∈N and ancilia qubit |b⟩ and gives |i⟩ and |b⊕xi⟩ where xi is the ith bit of input x.

Ox|i⟩|b⟩=|i⟩|b⊕xi⟩=(−1)b∗xi|i⟩|b⟩ (1)

This type of oracle is known as bit-flip oracle. It’s simply a unitary reversible mapping of (i,b)↦(i,b⊕xi). Such type of mapping is used beacuse the operations we do in quantum computation should be unitary. An interesting fact, you can easily get back to (i,b) from (i,b⊕xi) by simply applying the same oracle Ox to (i,b⊕xi) due to the fact that xi⊕xi=0 for any xi.

I wanted to talk about one more oracle known as phase oracle which is widely used in quantum algorithms. You can take this as a special case of bit flip oracle where ancilia qubit is |−⟩ . The qubit |−⟩ is simply |0⟩−|1⟩√2 . If we apply the bit flip oracle in this case, we can observe that the output would just changes the phase of our original state.

Ox|i⟩|−⟩=(−1)xi|i⟩|−⟩ (2)

# Query Complexity[](https://aman-agrawal01.github.io/posts/2021/11/query_complexity/#query-complexity "Permalink")

The query complexity is used in deterministic as well as quantum algorithms. One should note that there is a difference between query complexity of an algorithm and that of a function.

The query complexity of an algorithm would be the minimum number of queries that it takes to compute the function f(x) on any input x.

The query complexity of a function is the minimum number of queries that an optimal algorithm takes in order to compute function f(x) on any input x.

# Why Query Model?[](https://aman-agrawal01.github.io/posts/2021/11/query_complexity/#why-query-model "Permalink")

Now you might ask, why do we really need to know about query complexity? That’s a valid question to ask. There are couple of reasons that convince us to have an idea about query complexity.

Firstly, it’s easy to analyse and a lot of known quantum algorithms like Shor’s algorithm and Grover’s search are based on query model.

Secondly, it gives us a bound on time complexity of an algorithm. Finding the time complexity of a quantum algorithm is a tricky task but it turns out that if we are able to find the query complexity of the algorithm than we know that time complexity is larger than query complexity and hence gets some idea about the time complexity of an algorithm.

# Conclusion[](https://aman-agrawal01.github.io/posts/2021/11/query_complexity/#conclusion "Permalink") 

So, that’s it! Hope you like the blog :) I am planning to write one more blog on a result “the approximate degree gives a lower bound on quantum query complexity”.

<!--EndFragment-->