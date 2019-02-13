---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 4 - The Feature Space Laplacian Graph Kernel"
---
Probabilistically, the Laplacian graph kernel assumes that every graph is represented by a joint probability distribution that generates random vectors $$\mathbf{x} = (x_1,...x_n)^T$$. The kernel between two graphs therefore compares these vector generating distributions to calculate a metric of similarity.

Recall that one of our problems about the Laplacian graph kernel was the fact that it is sensitive to permutations. For example if two input graphs are exactly the same but the nodes are labeled in a different order, then the kernel fails to capture the similarity.

To gain *permutation invariance* the authors propose a simple trick, which actually will be very useful for *kernelizing* the proposed kernel (or recursively define) in the future. Lets try to recreate the thought process step by step:
1. The trick is based on the observation that if we work on variables that are defined in a vertex space, our kernel will always be sensitive to permutations. Because in a vertex space (obviously tied to a graph definition), variables are graph nodes and their order is implicitly defined by the topology of the graph that they reside in.
2. Therefore, we need a way to project vertex space variables onto a feature space which is permutation invariant. An extremely simple example for this could be instead of using a node as a variable, using a collection of its local features such as its degree. Of course hard coding these variables is not a good idea, and the authors have a very elegant trick for this that we will be discussing soon.
3. Lets introduce some notation for this projection operation. Let $$x_1,...x_n$$ be the vertex space variables, and $$y_1,...,y_m$$ be their projected counterparts or the feature space variables where $$y_i = \sum_j t_{i,j}(x_j)$$. In this equation, $$t_{i,j}$$ is a mapping function. There are a couple of things to note in here:
  - Number of variables in the vertex space $$n$$ is not necessarily equal to number of variables $$m$$ in the feature space. This means we are not necessarily looking for a one-to-one mapping between the elements of two spaces.
  - In fact, the mapping function $$t_{i,j}$$ is defined on edges $$i,j$$. Therefore feature space variables are summations of invariant features of a set of local neighborhoods (similar to [node2vec](https://cs.stanford.edu/~jure/pubs/node2vec-kdd16.pdf)'s neighborhood likelihood maximization).
  - $$t_{i,j}$$ is a transformation that depends on $$v_j$$'s permutation invariant properties. It can be a linear function like $$t_{i,j}(x_j) = \phi_i (v_j)\cdot x_j$$, where $\phi_i$ is a permutation invariant vertex feature.
4. 





**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
