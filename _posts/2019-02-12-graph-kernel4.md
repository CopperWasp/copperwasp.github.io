---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 4 - The Feature Space Laplacian Graph Kernel"
---
Probabilistically, the Laplacian graph kernel assumes that every graph is represented by a joint probability distribution that generates random vectors $$\mathbf{x} = (x_1,...x_n)^T$$. Note that the joint distribution takes both nodes and edges as parameters. Therefore, elements of a random vector $$\mathbf{x}$$ sampled from the joint distribution carries information from both nodes and edges of a graph. The Laplacian graph kernel between two graphs compares these vector generating joint distributions to calculate a metric of similarity.

Recall that one of our problems about the Laplacian graph kernel was its permutation sensitivity. For example, if two input graphs are exactly the same but their nodes are labeled in a different order, then the kernel fails to capture their similarity.

the authors propose a simple trick to gain *permutation invariance*, which actually will be very useful for *kernelizing* the proposed kernel (or recursively define) in the future. Lets try to recreate the thought process of the authors, step by step:
1. The trick is based on the observation that if we work on variables that are defined in a vertex space, our kernel will always be sensitive to permutations. For example, joint distributions of two isomorphic graphs can be evaluating the same nodes in different orders, therefore generating different vectors in the vertex space.
2. Therefore, we need a way to project vertex space variables onto a feature space using permutation invariant transformations. An extremely simple example for this could be instead of using a node as a variable, using a collection of its local features such as its degree to define a new variable. Of course hard coding these variables is not a good idea, and the authors have a very elegant trick for this that we will be discussing soon.
3. Lets introduce some notation for this projection operation from the vertex space onto a new feature space. Let $$x_1,...x_n$$ be the vertex space variables, and $$y_1,...,y_m$$ be their projected counterparts where $$y_i = \sum_j t_{i,j}(x_j)$$, and $$t_{i,j}(x_j)=\phi_i(v_j)\cdot x_j$$. This means every feature $$y_i$$ we define in the new feature space uses a weighted sum of all $$x_j$$ values, and the weights are determined by the mapping function $$\phi_i$$ of the feature $$y_i$$. The mapping function $$\phi_i$$ can be any local (permutation invariant) feature such as the degree of its input node. Note that the number of variables in the vertex space $$n$$ is *not necessarily* equal to number of variables $$m$$ in the feature space. This means we are *not necessarily* looking for a one-to-one mapping between the features of two spaces.
- For example, let the vector from the vertex space be $$\mathbf{x} = (x_1,...x_n)^T$$. Assume we want to map the vertex space variable onto a two dimensional feature space. Therefore we will only have two feature space variables $$y_1$$ and $$y_2$$.
- For each feature space variable $$y_i$$, define a $$\phi_i$$ (we won't need to do that once we kernelize the FLG kernel). For example let $$\phi_1$$ return the degree of its input vertex, and $$\phi_2$$ return the weight of its input vertex.
- Then, the value of the feature can be expressed as $$y_i = \sum_j \text{degree}(v_j)\dot x_j$$, where $$j$$ iterates over every vertex space variable.

4.  $$\sum_{i=1}^{n}$$





**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
