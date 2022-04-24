---
layout: post
title:  "Basic statistic knowledge"
date:   2022-04-17 15:00:00 +0000
categories: jekyll update
---

However, whereas the random samples of the integrand used in a conventional Monte Carlo integration are statistically independent (Reject-accept), those used in MCMC are autocorrelated. 

Calculate the expectation of a probability distribution is just to calculate the integral of the probabilty density function. In other words, the application of integral in probability theory.

## Traditional Monte Carlo (Random samples are independent)

### Rejection Sampling

Motivation:
For example, we can only simulate simple naive sampling like uniform distribution. Our computer has inbuilt function for it (even though this process is still pesudo random faked by a deterministic process).  How to get complicated sampling like exponential distribution? 

![avatar](./Image/Rejection_Sampling.png)

Comparing the difference between all the nodes and the accepted blue ones. For the whole set of black nodes (all the blue nodes and orange nodes), the values about x-axis of these nodes are distributed uniformly according to the uniform distributed. For the accepted blue node, the values about x-axis of these nodes are exponentially distributed. The propotion of these nodes in different positions in terms of x-axis follow the propotion that an exponential distribution should have. The uneven distribution in terms of y-axis of these nodes, is the reason why their values about x-axis follow the deserved propotion. while using these sampled nodes, their y-axis values become irrelevant and could be ignored.

cons: very inefficient, espicially when the dimension of distribution is high, large amounts of sampled points are wasted and abandoned.



## Markov Chain Monte Carlo (Random samples are autocorrelated) ? what autocorrelated means? Correlations of samples introduces the need to use the Markov chain central limit theorem when estimating the error of mean values.?

Monte Carlo method 是一种普遍的方法，应用在概率分布中，就成了rejection sampling（在考虑前后采样的random points彼此无关的情况下）
https://towardsdatascience.com/a-zero-math-introduction-to-markov-chain-monte-carlo-methods-dcba889e0c50


 If a randomly generated parameter value is better than the last one, it is added to the chain of parameter values with a certain probability determined by how much better it is (this is the Markov chain part).




### Gibbs sampling (One example of MCMC)

For multi-variable distribution, e.g. 5 variables, Choose a random point in this 5-dimensional space. Given 2nd to 5th variables fixed, sample the 1st variable according to the simple conditional distribution. Then keep the 1st, 3rd to 5th variables fixed, sample the 2nd variable according to its simple conditional distribution. Every 5 steps, we get a new sample point. With this method, the sample points belong to the 5-dimentional multi-variable distribution.
The philosophy and intuition behind is that the conditional distribution is much easier to sample from. The joint distribution is not.


### Metropolis hastings (One example of MCMC)

random choose a sample point, Sample a new sample point according to arbitary possible distribution ***f*** we could sample from. We adjust the acceptance probabilty according to balance stationary condition. Finally, the samples we have follow the target distribution ***p*** we want to sample from. Does the ***f*** and ***p*** only have to the difference of a constant?

Gibbs Sampling

This method requires all the conditional distributions of the target distribution to be sampled exactly.

A detailed description of MCMC as supplementary, which provides the explaination of the exsitence of constant ***N*** in ***p(x)=f(x)/N***, the ***N*** is userd to increase the accept rate as much as possible for better sampling efficiency to avoid rejection of samples as possible.

The exsitence of accept-reject rate is due to the difficulty of finding out the probability transition matrix ***P*** for our deserved stationary distribution ***Π***. The choice of ***P*** determines the final stationary distribution ***Π*** according to  ***PΠ=Π***. This is  another expression of the fixed-point theorm.

https://zhuanlan.zhihu.com/p/253784711

From the above perspective, reinforcement learning is trying to adjust the ***P*** by considering the policy and state transition function together as the ***P***  and adjust the policy part to adjust the whole ***P***, which lead to such a stationary distribution ***Π*** which provides maximum reward ***r(Π)***. It is also a kind of complicated markov chain monte carlo. The discovery of stationary distribution ***Π*** is also the arrival of fix-point.
