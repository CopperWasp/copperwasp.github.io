---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 4 - The Feature Space Laplacian Graph Kernel"
---
Probabilistically, the Laplacian graph kernel assumes that every graph is represented by a joint probability distribution that generates random vectors $$\mathbf{x} = (x_1,...x_n)^T$$. Note that the joint distribution takes both nodes and edges as parameters. Therefore, elements of a random vector $$\mathbf{x}$$ sampled from the joint distribution carries information from both nodes and edges of a graph. The Laplacian graph kernel between two graphs compares these vector generating joint distributions to calculate a metric of similarity.

Recall that one of our problems about the Laplacian graph kernel was its permutation sensitivity. For example, if two input graphs are exactly the same but their nodes are labeled in a different order, then the kernel fails to capture their similarity.

the authors propose a simple trick to gain *permutation invariance*, which actually will be very useful for *kernelizing* the proposed kernel (or recursively define) in the future. Lets try to recreate the thought process of the authors, step by step:
1. The trick is based on the observation that if we work on variables that are defined in a vertex space, our kernel will always be sensitive to permutations. For example, joint distributions of two isomorphic graphs can be evaluating the same nodes in different orders, therefore generating different vectors in the vertex space.
2. Therefore, we need a way to project vertex space variables onto a feature space using permutation invariant transformations. An extremely simple example for this could be instead of using a node as a variable, using a collection of its local features such as its degree to define a new variable. Of course hard coding these variables is not a good idea, and the authors have a very elegant trick for this that we will be discussing soon.
3. Lets introduce some notation for this projection operation from the vertex space onto a new feature space. Let $$x_1,...x_n$$ be the vertex space variables, and $$y_1,...,y_m$$ be their projected counterparts where $$y_i = \sum_j t_{i,j}(x_j)$$, where $$t_{i,j}(x_j)=\phi_i(v_j)\cdot x_j$$ (Each feature in space $$y_i$$ uses a mixture of all mapped(features) in vertex space, also there is a mapping $$\phi_i$$ for each $$y_i$$) In this equation, $$t_{i,j}$$ is a mapping function. There are a couple of things to note in here:
  - Number of variables in the vertex space $$n$$ is not necessarily equal to number of variables $$m$$ in the feature space. This means we are not looking for a one-to-one mapping between the elements of two spaces.
  - In fact, the mapping function $$t_{i,j}$$ is defined on edges $$i,j$$. Therefore feature space variables are summations of invariant features of a set of local neighborhoods (similar to [node2vec](https://cs.stanford.edu/~jure/pubs/node2vec-kdd16.pdf)'s neighborhood likelihood maximization).
  - $$t_{i,j}$$ is a transformation that depends on $$v_j$$'s permutation invariant properties. It can be a linear function like $$t_{i,j}(x_j) = \phi_i (v_j)\cdot x_j$$, where $\phi_i$ is a permutation invariant vertex feature.
4.  $$\sum_{i=1}^{n}$$





**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
