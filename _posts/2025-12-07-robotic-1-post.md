---
layout: post
title: "Robotic 001"
description: "Notes on learning MIT robotic manipulation"
modified: 2025-12-07 11:32:00 -0800
tags: [Robotic]
image:
  feature: 
  credit: 
  creditlink: 
comments: 
share: 
---

## Resources

- [6.4210 MIT Book](https://manipulation.csail.mit.edu/)

## Preliminary

Basic control notations 

$$
\begin{aligned}
q &= \text{state, position} \\
\dot{q} &= \text{velocity} \\
\ddot{q} &= \text{acceleration}
\end{aligned}
$$

The fundamental problem about control is given a target position or velocity, what the applied force should be. 

For example, PID controls lays out the following: 

$$
\tau = k_p (q^d - q) + k_d (\dot{q}^d - \dot{q}) +
        k_i \int (q^d - q) dt,
$$

where $*^d$ is desired position/velocity and $tau$ is the applied torque needed. The interpretation is that, the closer $q$ is toward the target position, the applied force is lower.

The fundamental problem in robotic is then given the target position/velocity, what are the appleid forces for each joint. For example a robotic arms can have high-single digit or double digit joints, what's the commanded force should be moving A=>B or higher level task of opening a door.


## Pick and Place

The class starts with a setup that a robotic arm need to pick a brick and place it to a target position.

![png](pick.png)