+++
title = "Circle detection: a recursive perspective"
date = 2026-10-18
extra.toc = true
extra.katex = true
[taxonomies]
tags = ["programming", "algo", "math"]
+++

I love recursive way of interpreting common algorithms but the Floyd’s algorithm has been an exception for a long time.
The main obstacle is that if a linked list has circle, we may not be able to confirm that our recursion can terminate.
In other words, The linked circle simply has no base case!

It seems that if we have to adopt the recursive view, we have to memorize all visited nodes which has `O(n)` space complexity which is not ideal. However, today, I successfully find the valid recursive interpretation of Floyd’s algorithm and while I was using this view, I also discovered another interesting algorithm.


## The baseline
Before we gei into the optimal space algorithm, let's review our most naive baseline algorithm.
This naive algorithm just memorizes all visited nodes and if the current nodes is equal to one of the visited nodes, we terminate and returns true. Otherwise, we shall encounter nil, meaning the list has no circle and returns false.

The whole algorithm has a naive recursive interpretation which is just decomposing the problem along the input list.


## The recursive structure
Now let's face the hard part.

The naive algorithm's bigest flaw is that it may use too much memory space.
We want to use just `O(1)` space complexity but this seems quite hard..

Traditional guides now will introduce the concept of fast-slow pointers and use the fact that the fast pointer will end up meeting the slow one in a circle. Although this explanation seems intuitive but it's somewhat strange. Maybe, I mean maybe, we can still find a recursive algorithm which still uses `O(1)` space.

In out baseline setting, we put that the recursive data structure is the input linked list. However, if we do recursion just ont the list, we may lose too much information which may be necessary for circle detection. Instead, we introduce an extra state to indicate the circumference or a interval limit of the detected circle.

Formally, suppose we have a state $(c, p)$, the subproblem $f(c, p)$ means that starting from the node $c$, does it exist a circle with circumference $>= p$. Note that by 'starting from the node $c$', we means that the actual node in the circle may be some node AFTER node $c$.

Now, let's solve the whole problem based on this kind of subproblem.
Suppose we are on the current node $c$, we need to return whether there's a circle with length larger or equal to $p$ after $c$.
Then, we simple check the node $c' = c + p$, which is the node $p$ steps after $c$.

If $c = c'$, we can confirm that we have detected a circle and just returns true.
Otherwise, we have several possibilities. 
First, the node $c$ may be outside the circle. 
Second, if $c$ is already in a circle, the circle's length is not $p$.
These 2 possibilities can be handled just to another subproblem $f(next(c), p + 1)$. 
If we step our current node, the node will eventually enter the circle or just stumble upon nil and while we are incresing the interval $p$, we will finally reach the true length of the circle because the interval will repeatedly module the length of the circle and traverse all values less than or equal to the true length. Therefore, the final formula is

$$
f(c, p) \rightarrow f(next(c), p + 1)
$$

This recursive formula is just eqvivalent to Floyd’s algorithm!
Notice that in Floyd’s algorithm, the distance between the fast pointer and the slow one increase 1 in every step, which just means that the interval increase in each step and the slow pointer is just our 'current pointer' in the recursive view.


## Brent's algorithm

Contemplating on the subproblem $f(c, p)$, do we have to divide the problem like Floyd’s way?
Maybe, we can use another strategy.

I don't have enough time to explan this strategy in detail, but we just divide like

$$
f(c, p) -> f(next^n(c), 2p)
$$

which surprisingly, connects directly to the Brent's algorithm.


