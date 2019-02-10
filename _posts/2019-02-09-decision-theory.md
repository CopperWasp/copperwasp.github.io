---
layout: post
title:  "Notes on Decision Theory 1: Motivation"
---
Uncertainty is at the core of machine learning systems. We use probability theory to quantify and manipulate uncertainty. This turns uncertainty from something we are afraid of to something we can make use of.

Most machine learning problems involve making *optimal decision*. For example, given a set of hospital records we might need to create systems that are able to decide if a patient is sick. Or given a set of statistics about houses such as *number of rooms* and *location*, our system might need to decide what is the most appropriate *price* for a given house.

We make use of probability theory to clarify and also generalize problem definitions. This gives us the chance to use mathematical tools and tricks towards solving a given problem.

We can for example, restate the decision problem with hospital records as follows:
- Given a set of samples from the joint distribution $$p(\mathbf{x},y)$$ where $$\mathbf{x} \in \mathbb{R}^d$$ and $$y \in \{0,1\}$$, learn a separating function that is able to correctly divide unseen samples from the same distribution. Note that $$\mathbf{x}$$ carries the information provided by the hospital records, and $$y$$ encodes if a patient is sick or not.

In this case we are interested in the value of $$y$$ that maximizes $$p(y \vert \mathbf{x})$$. The intuition is to see if probability of being sick is higher than being healthy given the records, and *decide* accordingly. **Is this intuition always correct?**
*These notes are products of self studies from several machine learning resources.*
