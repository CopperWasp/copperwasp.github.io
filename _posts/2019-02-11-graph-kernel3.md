---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 3 - Laplacian Graph Kernels"
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

The laplacian matrix is positive semi-definite ($$\mathbf{z}^T L \mathbf{z} \geq 0$$ if $$\mathbf{z}$$ is nonzero), which roughly means *the direction of nonzero vector processed by this matrix will not change sign*. Graph Laplacian can also be expressed in terms of the degree matrix D and the adjacency matrix A as $$L=D-A$$, which supports the *discrete second derivative* intuition. Graph Laplacian contains useful information about a graphs features, just like different moments of a function contain useful information about the function ([e.g. we can approximate a function by an infinite sum of its derivatives](https://en.wikipedia.org/wiki/Taylor_series)).

Spectral graph theory suggest that eigenvectors with low eigenvalues of a graph Laplacian provides information about the overall graph topology. The authors of this paper provided two ways to confirm this.
1. For any vector $$\mathbf{z} \in \mathbb{R}^n$$, $$\mathbf{z}^T L^G \mathbf{z} = \sum_{\{i,j\} \in E}w_{i,j}(z_i - z_j)^2$$. How do we interpret this equation?
- First its important to realize that given equation is the quadratic form of Laplacian. In fact, the definition of Graph Laplacian is [designed to capture this quadratic equality](http://www.cs.yale.edu/homes/spielman/561/2012/lect02-12.pdf), so that it can operate like a *discrete derivative*.
- Still, why do we think low eigenvalue eigenvectors give global information about a graph? An intuitive way to explain this could be following. Assume that $$\mathbf{z}$$ is an eigenvector of the Laplacian $$L^G$$. If its a low eigenvalue eigenvector then $$(z_i - z_j)^2$$ component of the Laplacian quadratic form will be small, overall. Which means the eigenvector $$z$$ is a smooth function (will not easily change value when small/local changes happen in its input).
- Since we already know eigenvectors of Laplacian carry information about the graph, and low eigenvalue eigenvectors are insensitive to local changes, they must be carrying some information in a more global level.
2. Another way to confirm this intuition is using a Gaussian graphical model over $$n$$ variables ($$x_1,...,x_n$$) to construct the graph $$G$$.
- Assume for each edge and vertex the clique potentials are $$\phi(x_i,x_j)=e^{-w_{i,j}(x_i-x_j)/2}$$ and $$\psi(x_i)=e^{-\eta {x^2}_i/2}$$ respectively. In other words, if the weighted difference between a pair of nodes is small, then the clique potential is higher. A similar logic applies for the vertex based potential.
- Given the potentials, the joint distribution $$\mathbf{x}$$ is proportional to (not exactly equal because we don't know how the cliques are factorized) multiplication of potentials for each node and edge. Which ends up being $$e^{-\mathbf{x}^T(L+\eta I)\mathbf{x}/2}$$, after rearranging.
- This is an interesting outcome since it shows that the covariance matrix of $$\mathbf{x}$$ is $$(L^G + \eta I)^{-1}$$. Since small eigenvalue eigenvectors of a covariance matrix represent the direction of the points with a smaller spread (in terms of variance), this direction applies to a large fraction of points therefore represents a more global information.
- This is kind of the opposite of the logic that we use for SVD in dimensionality reduction tasks. We select large eigenvalue eigenvectors since they carry a more discriminative information: direction the points differ the most.

The intuitions given above suggest that if we want a kernel that is able to compare two graphs in terms of their overall topology, it is a good idea to consider comparing lower eigenvalue eigenvectors of given graphs.

Further expanding the Markov Random Field intuition, assume graphs $$G_1$$ and $$G_2$$ with $$n$$ vertices represented by normal distributions $$p_1 = \mathcal{N}(0,L^{-1}_1)$$ and $$p_2 = \mathcal{N}(0,L^{-1}_2)$$ respectively.
- Note that as our basis we will use the [Bhattacharyya kernel](http://www.jmlr.org/papers/volume5/jebara04a/jebara04a.pdf) $$k(p_1,p_2) = \int \sqrt{p_1(x)}\sqrt{p_2(x)}dx$$, because it has a closed form for Gaussian distributions. This kernel acts like a symmetric approximation to KL Divergence, measuring the similarity (*affinity*) between probability distributions.
- In our case, Bhattacharyya kernel's closed form for Gaussians is $$\begin{equation}
k(p_1,p_2) = \dfrac{\lvert (\dfrac{1}{2}L_1 + \dfrac{1}{2}L_2)^{-1} \rvert^{1/2}}{\lvert L_1^{-1} \rvert^{1/4}\lvert L_2^{-1} \rvert^{1/4}}\end{equation}$$.
- We need to make one final observation to be able to completely define the Laplacian graph kernel. If some of the eigenvalues of $$L_1^{-1}$$ or $$L_2^{-1}$$ are very small, some kernel values can be vanishingly small because of the multiplicative nature of the Bhattacharyya kernel. To solve this problem, we additively regularize $$L_1^{-1}$$ and $$L_2^{-1}$$ defining $$S_1 = L_1^{-1} + \gamma I$$ and $$S_2 = L_2^{-1} + \gamma I$$, where $$\gamma$$ is a small constant.
- Now we can define the Laplacian graph kernel (LG kernel) as $$\begin{equation}
k_{LG}(G_1,G_2) = \dfrac{\lvert (\dfrac{1}{2}S_1 + \dfrac{1}{2}S_2)^{-1} \rvert^{1/2}}{\lvert S_1^{-1} \rvert^{1/4}\lvert S_2^{-1} \rvert^{1/4}}\end{equation}$$.

The very first thing we observe about this kernel is value of integral is mostly determined by the eigenvectors of $$L_1^{-1}$$ and $$L_2^{-1}$$ that have large eigenvalues and aligned. Since it depends on the eigenvectors of **inverted laplacian matrices**, it captures the similarity between overall shapes of $$G_1$$ and $$G_2$$.

The problems of LG kernel we will be addressing address in the next post are:
-  It assumes that both graphs have same number of vertices,
-  It is only sensitive to global structure of the graphs,
-  It is not a permutation invariant kernel, therefore can't measure the similarity between isomorphic (sub)graphs accurately.

**References**  
[Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).](https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf)
