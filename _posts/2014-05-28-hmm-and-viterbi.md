---
layout: post
title: "HMM and Viterbi"
description: "A notes on reading standford cs229 ML course"
modified: 2014-05-28 20:58:37 -0400
category: [Machine Learning ]
tags: []
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: 
---
[stanford Handout](http://cs229.stanford.edu/section/cs229-hmm.pdf)

# MARKOV ASSUMPTION

#### Limited horizon assumption: not depend on whole history 
$$P(z_t|z_{t-1} ...z_1) = P(z_t|z_{t-1})$$

#### Stationary process assumption: transition is not depend on time
\\[P(z_t|z_{t-1}) = P(z_2|z_1)\quad t\in 2...T\\]

# Transition Matrix
The model need to maximize the log-likehood of the state sequence for transition matrix.\\( \vec{z}\\) is the state sequence and $A$ is transition matrix.
\\[\log P(\vec{z};A)\\]
By the Lagrangian Multiplier, the optimal solution is given by 
$$A_{ij}=\dfrac{\sum_{t=1}^T1\{z_{t-1}=s_i\wedge z_t=s_j\}}{\sum_{t=1}^T1\{z_{t-1}=s_i\}}$$
