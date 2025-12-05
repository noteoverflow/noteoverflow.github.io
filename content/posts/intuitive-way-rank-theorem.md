+++
title = "An intuitive understanding matrix rank theorem"
date = 2025-12-05
extra.katex = true
extra.toc = true
[taxonomies]
tags = ["math", "linear_algebra"]
+++

The theorem of equality of matrix row rank and column rank if well known.
However, the conclusion seems somehow surprising and mysterious.
Traditional proofs are based on elimination or dual spaces but I found the decomposition way is much simpler and more intuitive.

Our goal:
> **Theorem of rank**:  
> Given any matrix $A$, $rank(A) = rank(A^T)$

where $rank$ means the number of independent columns.

<br/>

## Extended identity
> **Lemma 1**:  
> Given an identity matrix I, $rank(I) = rank(I^T)$

This lemma is so obvious that no proof needed.

> **Lemma 2**:  
> No matter how many columns added into an identity matrix I, rank of the extended matrix E does not change.  
> i.e., $rank(E) = rank(I)$

<br/>


## CR Decomposition
With above lemmas ready, we can finally prove the goal theorem.

Given a matrix $A$, we can choose all indenpendent columns and form it as a new matrix $C$.
For example:

$$
A = \begin{bmatrix}
    0 & 1 & 1\\\\
    1 & 0 & 2
\end{bmatrix}
$$

Then

$$
R = \begin{bmatrix}
    0 & 1\\\\
    1 & 0
\end{bmatrix}
$$

Now, notice that matrix $C$ already contains all necessities to recover matrix $A$ 
since we can compose dependent columns by composing indenpendent columns in $C$ linearly.
The recovering process can be represented as a right-multplied matrix $R$:

$$
A = CR
$$

Since matrices $C$ and $R$ always exists in any matrices, we call this kind of decomposition **CR Decomposition**.

How does this relate to the rank theorem?
Notice that the matrix $C$ can also be seen as row compositions of matrix $R$!
Let's make the dimensions of above matrices clear:

$$
A: m \times n\\\\
C: m \times k, \\
R: k \times n
$$

where $k \leq n$.

Now that rows of $A$ are row compositions of $R$, then

$$
rank(A^T) \leq rank(R^T)
$$

Since we aleady know

$$
rank(A) = rank(C) = k
$$

We next need to prove that $rank(R^T) = k$, which means all rows of $R$ are independent.

Remember that columns of $C$ are selected from $A$.
Then we can ensure that, in matrix $R$, we at least has an inner identity inside $R$.

> **Theorem**:
> $R$ is an extended identity.

The proof is quite obvious.

<br/>

## Dual the two halfs!

Now we know that

$$
rank(A^T) \leq rank(R^T) = k = rank(C) = rank(A)
$$

which is a half of the final rank theorem!
Surprisingly, if we choose indenpendent rows instead of columns or just transpose $A$ in the first place,
then the next half can be achieved automatically:

$$
rank(A) \leq rank(A^T)
$$

Finally:

$$
rank(A^T) \leq rank(A) \leq rank(A^T)\\\\
\Rightarrow rank(A) = rank(A^T)
$$