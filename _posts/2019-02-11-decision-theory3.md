---
layout: post
title:  "Notes on Decision Theory 3: Expected Loss"
---
Directly minimizing the misclassification rate might not be desirable in certain situations. For example, diagnosing a cancer patient as healthy is usually a bigger mistake than diagnosing a healthy person as cancer. Therefore we need to clarify the difference between the consequences of different types of misclassification.

We use *loss functions* to quantify the severeness of a misclassification. Therefore we want to minimize the total loss over all instances we tried to classify. The problem is, we can not directly minimize the loss function because it is defined on the true distribution $$p(\mathbf{x}, y)$$ that generates the data. Since we only have samples from this distribution, we minimize the expected loss:
- $$E[L] = \sum_{true}\sum_{pred}\int_{R_{pred}}L_{true,pred}p(\mathbf{x},y=true)d\mathbf{x}$$,  
where each $$L_{true,pred}$$ represents the amount of loss given a pair of true label and prediction values.
- For example, $$L_{healthy,cancer} = 10$$ and $$L_{cancer,healthy} = 1000$$.  

According to this formulation, we can see the problem of minimizing $$E[L]$$ as choosing an appropriate $$R_{j}$$ for each instance that minimizes $$\sum_{true} L_{true,pred}p(\mathbf{x}, y=true)$$. In other words for each instance, we want to predict a region that makes us suffer the least loss. We can again rewrite this as $$p(y=true \vert \mathbf{x})p(x)$$ and minimize $$\sum_{true}L_{true,pred}p(y=true \vert \mathbf{x})$$.

*These notes are products of self studies from several machine learning resources.*
