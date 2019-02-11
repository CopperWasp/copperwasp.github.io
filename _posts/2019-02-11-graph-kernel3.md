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
      0, & \text{otherwise}
    \end{cases}
\end{equation}$$




**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
