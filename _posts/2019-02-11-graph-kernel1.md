---
layout: post
title:  "Paper Summary: The Multiscale Laplacian Graph Kernel 1 - Motivation"
---
Traditional machine learning methods assume that the instances from an input space are *independently and identically distributed (i.i.d.)*. Therefore these algorithms do not try to capture the dependencies between instances. However the input space of a wide range of problems are spaces of graphs. Consequently, additional to individual information, their instance spaces can also contain inter-instance dependencies. In this case, using traditional methods working under the i.i.d. assumption may perform bad because of poor utilization of the data.

Some examples with graph-based input spaces are:
- Social networks: Dependency between individuals,
- Chemoinformatics: Dependency between molecules,
- Citation networks: Dependency between publications,
- Communication networks: Message passing represented as dependency.

One of the popular learning paradigms from graphs is *kernel-based learning*, especially because kernel methods separate the problems of learning a new data representation from learning an estimator (*e.g. classifier*). In general, a graph kernel must satisfy the following requirements:
- The kernel $$k(G_1, G_2)$$ should be able to capture the similarity between the graphs $$G_1$$ and $$G_2$$ sufficiently. Note that the definition of similarity may change based on what input data represents.
- The kernel $$k$$ must be invariant to order of vertices of its input graphs: $$k(G_1, G_2) = k(G_1, P G_2 P^T)$$, where $$P$$ is a permutation matrix. This is useful to capture the similarity between graphs with isomorphic (sub)structures.

Graph invariants are important (specifically in graph kernel literature and more generally graph related pattern recognition tasks) because they help us to extract **features that are general enough** to be useful for pattern recognition tasks in graphs. Efficiently computable graph invariants roughly fall in 2 categories:
- **Local invariants:** They represent local properties such as number of triangles, squares etc. that appear in a graph $$G$$.
- **Spectral invariants:** They carry information in a more *global* level. Usually expressed as functions of the eigenvalues of a graphs Laplacian or adjacency matrix.

**References**
*Kondor, R. and Pan, H., 2016. The multiscale laplacian graph kernel. In Advances in Neural Information Processing Systems (pp. 2990-2998).*
https://papers.nips.cc/paper/6135-the-multiscale-laplacian-graph-kernel.pdf
