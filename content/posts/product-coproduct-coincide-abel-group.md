+++
title = "Product and coproduct coinsides in the category of Abelian groups"
date = 2025-12-12
extra.katex = true
[taxonomies]
tags = ["math", "category-theory", "algebra"]
+++


It's rather beautiful that **product** and **coproduct** (sum) coinsides in the category of Abelian groups.
Recall that *product* object is a universal construct which satisfies a spectial pattern:

> Given two groups $A, B$, there can be constructed a product object $A \times B$ 
> with two projections $p$ and $q$ so that $p(a, b) = a$ and $q(a, b) = b$.

The product must satisfy a universal property which can be demostrated as the following commutative graph:
<br/>
<center>
{{ figure(id="/img/blog/product-universal.svg") }}
</center>

Accroding to above graph, given any group $X$ with projections:
<center>
$f: X \rightarrow A$ and 
$g: X \rightarrow B$
</center>

there exists unique homomorphism $h: X \rightarrow A \times B$ satisfying
<center>
$p \circ h = f$ and
$q \circ h = g$.
</center>

Apparently, $h$ can be defined as:
<center>
$h(x) = (f(x), g(x))$
</center>

Now, let's prove that the product constructed above is also a coproduct is all groups are abelian.

First of all, we define two injections:
<center>
$i: A \rightarrow A \times B,\ i(a) = (a, 0)$

$j: B \rightarrow A \times B,\ j(b) = (b, 0)$
</center>

Given other injections:
<center>
$f: A \rightarrow X$ and $g: B \rightarrow X$,
</center>

We need to find a unique morphism $h: A \times B \rightarrow X$ so that
<center>
$h \circ i = f$ and
$h \circ j = g$
</center>

Fortunately, $h$ can be defined as
<center>
$h(a, b) = f(a) + g(b)$
</center>

It's easy to verify that $h$ is a homomorphism:  

$h(a_1​,b_1​)+h(a_2​,b_2​)$  
$= f(a_1​)+g(b_1​)+f(a_2​)+g(b_2​)$  
$= f(a_1​+a_2​)+g(b_1​+b_2​)$  
$= h((a_1​,b_1​)+(a_2​,b_2​))$

and
<center>
$h \circ i​(a) = h(a,0) = f(a)$  

$h \circ j​(b) = h(0,b) = g(b)$
</center>