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
Artificial Intelligence: A Modern Approach(R&N) chap 15

# MARKOV ASSUMPTION

#### Limited horizon assumption: not depend on whole history 
\\[P(z\_t|z\_{t-1} z\_{t-2} ...z\_1) = P(z\_t|z\_{t-1})\\]

#### Stationary process assumption: transition is not depend on time
\\[P(z_t|z_{t-1}) = P(z_2|z_1)\quad t\in 2...T\\]

# Transition Matrix
The model need to maximize the log-likehood of the state sequence for transition matrix.\\( \vec{z}\\) is the state sequence and $A$ is transition matrix.
\\[\log P(\vec{z};A)\\]
By the Lagrangian Multiplier, the optimal solution is given by 
\\[A\_{ij}=\dfrac{\sum\_{t=1}^T1\\{z\_{t-1}=s_i\wedge z_t=s_j\\}}{\sum\_{t=1}^T1\\{z\_{t-1}=s_i\\}}\\]

# HMM INTUITION
Both [wiki](http://en.wikipedia.org/wiki/Viterbi_algorithm) and R&N have a good example that illustrate the intuition of HMM. Basically, we have known observation sequence and unknown state sequence. As an example in wiki, the known observation sequence is the patient feeling(normal, cold, dizzy) and the unknown state sequence is the health condition of the patient(Healthy, Fever). Below is the image in wiki Viterbi algorithm.
![alt tag]({{site.url}}/images/An_example_of_HMM.png)
By the probability of state transition(P(Healthy->Fever)) and emission matrix of state to observation(P(Normal|Healthy)), we are able to approximate the state sequence or predict the next state or maybe next observation based on the specific tasks.


