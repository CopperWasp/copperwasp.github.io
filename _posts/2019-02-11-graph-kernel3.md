---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 2 - Laplacian Graph Kernels"
---
Before diving into the technical details of the proposed method, let us introduce some notation and review relevant background.
- Let $$G(V,E)$$ be a weighted undirected graph, where $$V = \{v_1,...,v_n\}$$.
- Laplacian $$L^G$$ of $$G$$ is an $$n \times n$$ matrix with indices defined as:
$$\begin{equation}
  L^{G}_{i,j} =
    \begin{cases}
      -w_{i,j}, & \text{if}\ \{v_i,v_j\} \in E\\
      \sum_{j:\{v_i,v_j\}\in E^{w_{i,j}}}, & \text{if}\ i=j\\
      0, & \text{otherwise,}
    \end{cases}
\end{equation}$$  
where $$w_{i,j}$$ is the weight of the edge $$\{v_i,v_j\}$$.  

Laplacian is an operator just like divergence, gradient and derivate are operators too. Intuitively Laplacian is like a second-derivative in a discrete space (graph). It is defined as the *divergence of the gradient of a function*:
- Gradient of a multivariate function will give you a gradient field, made of gradient vectors at different points of the function.
- Divergence of a gradient field will give you a metric that measures the outwards movement (in terms of gradient directions) evaluated at each point.

The laplacian matrix is positive semi-definite ($$z^T L z \geq 0$$ if $$z$$ is nonzero), which roughly means *the direction of nonzero vector processed by this matrix will not change sign*. Graph Laplacian can also be expressed in terms of the degree matrix D and the adjacency matrix A as $$L=D-A$$, which supports the *discrete second derivative* intuition. Graph Laplacian contains useful information about a graphs features, just like different moments of a function contain useful information about the function ([e.g. we can approximate a function by an infinite sum of its derivatives](https://en.wikipedia.org/wiki/Taylor_series)).

Spectral graph theory suggest that eigenvectors with low eigenvalues of a graph Laplacian provides information about the overall graph topology. The authors of this paper provided two ways to confirm this.
1. For any vector $$z \in \mathbb{R}^n$$, $$z^T L^G z = \sum_{\{i,j\}\inE}w_{i,j}(z_i - z_j)^2$$.







**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
