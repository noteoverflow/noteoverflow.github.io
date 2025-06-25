+++
title = "Error handling done wrong"
# date = 2025-06-25
extra.toc = true
extra.katex = true
+++

Error handling is hard.
Various programming languages have various kinds of error handling patterns.
Is there an optimal way of error handling?

> This post only consists of personal thoughts.
> Many opinions may be wrong.

## Error handling as effect
In general, error handling can be seen as one kind of spectial computational *effect*.
The effect can be modeled as:

$$
f : a \rightarrow_m b
$$

where $m$ is the effect that function $f$ will produce when invoked.
If we focus on error handling, $m$ can be further delineated as:

$$
f : a\rightarrow_{m(e)} b
$$
where $e$ denotes the error type.

All these concepts are all too abstract. Let's demonstrate some examples.

## Effect as Higher-Kinded Type

### Product

### Optional effect

### Error code

### Exception

### Hybrid effect


## Effect as Monad

### Free monad


## Effect as Algebraic Effect

### Algebraic Effect as coroutine


