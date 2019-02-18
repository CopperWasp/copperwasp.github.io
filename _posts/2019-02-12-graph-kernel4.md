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
- For each feature space variable $$y_i$$, define a $$\phi_i$$ (we won't need to do that once we kernelize the FLG kernel, hang on for now). For example let $$\phi_1$$ return the degree of its input vertex, and $$\phi_2$$ return the weight of its input vertex.
- Then, the value of the feature can be expressed as $$y_i = \sum_j \text{degree}(v_j)\cdot x_j$$, where $$j$$ iterates over every vertex space variable.
4. Lets put these together in a more compact form. As long as we define a linear transformation between two spaces, such as a dot product as we did above, [the result will still be a multivariate normal random variable](http://www.cs.columbia.edu/~liulp/pdf/linear_normal_dist.pdf). Therefore, defining $$U_{i,j} = \phi_i(v_j)$$ and $$\textbf{y} = U \textbf{x}$$, we have $$\mathbb{E}(\mathbf{y})=0$$ and $$\text{Cov}(\mathbf{y},\mathbf{y}) = U \text{Cov}(\mathbf{x},\mathbf{x})U^T = UL^{-1}U^T$$.

Now we can define the *Feature Space Laplacian Graph Kernel (FLG Kernel)*, by replacing the vertex space variables we defined in *Laplacian Graph Kernel* with the feature space variables we defined above. Let $$S_1 = U_1 L_1^{-1} U^T_1 + \gamma I$$ and $$S_2 = U_2 L_2^{-1} U^T_2 + \gamma I$$. Then,
$$\begin{equation}
k_{LG}(G_1,G_2) = \dfrac{\lvert (\dfrac{1}{2}S_1 + \dfrac{1}{2}S_2)^{-1} \rvert^{1/2}}{\lvert S_1^{-1} \rvert^{1/4}\lvert S_2^{-1} \rvert^{1/4}}\end{equation}$$.

So, why do we like the FLG Kernel better?
1. It is permutation invariant, since its variables are defined by local vertex features.
2. Now that we work on a feature space that is independent from the graph size, we can apply the kernel to two graphs with different number of vertices.
**Note the the FLG Kernel still works in a single scale.** We will address this problem in the next post.


**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
