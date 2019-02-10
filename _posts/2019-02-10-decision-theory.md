---
layout: post
title:  "Notes on Decision Theory 2"
---

We can approach the problem of learning a separating function given a labeled dataset (such as the hospital data example from the previous post) as **learning a decision boundary with the minimum misclassification rate.** A decision boundary in this case, will try to predict the region each instance $$\mathbf{x}$$ resides in, by labelling them with either $$y=0$$ or $$y=1$$.

Assume instances provided with label 0 reside in the region $$R_0$$, and label 1 in the region $$R_1$$. We can express the misclassification probability of our classifier for new instances as
\$$p(error) = p(\mathbf{x} \in R_1, y=0) + p(\mathbf{x} \in R_0, y=1) = \int_{R_1}p(\mathbf{x}, y=0)d\mathbf{x} + \int_{R_0}p(\mathbf{x}, y=1)d\mathbf{x}$$.

In other words, it is the total probability of being labeled wrong by the classifier.





*These notes are products of self studies from several machine learning resources.*
