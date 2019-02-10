---
layout: post
title:  "Notes on Decision Theory"
---

Uncertainty is at the core of machine learning systems. We use probability theory to quantify and manipulate uncertainty. This turns uncertainty from something we are afraid of to something we can make use of.

Most machine learning problems involve making *optimal decision*. For example, given a set of hospital records we might need to create systems that are able to decide if a patient is sick. Or given a set of statistics about houses, such as *number of rooms* and *location* our system might need to decide what is the most appropriate *price* for a given house.

We make use of probability theory to clarify and also generalize problem definitions. This gives us the chance to use mathematical tools and tricks towards solving a given problem.

We can for example, restate the decision problem given hospital records as follows:
- Given a set of samples from the joint distribution p(x,y) learn a separating function that can correctly divide samples with different values of y.
$$ \begin{equation} \int_0^x \sin(x) dx \label{eq:test} \end{equation} $$
