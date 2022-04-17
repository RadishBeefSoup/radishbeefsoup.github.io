---
layout: post
title:  "Convex Optimization Learning!"
date:   2022-04-17 15:00:00 +0000
categories: jekyll update
---

Rejection Sampling

Motivation:
For example, we can only simulate simple naive sampling like uniform distribution. Our computer has inbuilt function for it (even though this process is still pesudo random faked by a deterministic process).  How to get complicated sampling like exponential distribution? 

![avatar](./Image/Rejection_Sampling.png)

Comparing the difference between all the nodes and the accepted blue ones. For the whole set of black nodes (all the blue nodes and orange nodes), the values about x-axis of these nodes are distributed uniformly according to the uniform distributed. For the accepted blue node, the values about x-axis of these nodes are exponentially distributed. The propotion of these nodes in different positions in terms of x-axis follow the propotion that an exponential distribution should have. The uneven distribution in terms of y-axis of these nodes, is the reason why their values about x-axis follow the deserved propotion. while using these sampled nodes, their y-axis values become irrelevant and could be ignored.

cons: very inefficient, espicially when the dimension of distribution is high, large amounts of sampled points are wasted and abandoned.

