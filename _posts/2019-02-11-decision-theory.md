---
layout: post
title:  "Notes on Decision Theory 3: Risk"
---
Directly minimizing the misclassification rate might not be desirable in certain situations. For example, diagnosing a cancer patient as healthy is usually a bigger mistake than diagnosing a healthy person as cancer. Therefore we need to clarify the difference between the consequences of different types of misclassification.

We use *loss functions* to quantify the severeness of a misclassification. Therefore we want to minimize the total loss over all instances we tried to classify. The problem is, we can not directly minimize the loss function because it is defined on the true distribution $$p(\mathbf{x}, y)$$ that generates the data. Since we only have samples from this distribution, we minimize the expected loss or *risk*:
- $$E[L] = \sum_{org}\sum_{pred}\int_{R_{pred}}L_{org,pred}p(\mathbf{x},y=org)d\mathbf{x}$$



*These notes are products of self studies from several machine learning resources.*
