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

和压缩映射的关系？


Bayesian Estimation

1. Point estimation (e.g. maximum likelihood estimation, guess the parameter(regarded as one constant) directly)
2. Interval estimation (e.g. Bayesian estimation, guess the parameter of the distribution of the parameter(regarded as one random varible, a distribution))
https://www.youtube.com/watch?v=I4dkEALQv34&t=2s


The flaw of frequenist statistic:
Dependence of the result of an experiment on the number of times the experiment is repeated.

P-value: The likelihood the observed fact happen by accident.

1. p-values measured against a sample (fixed size) statistic with some stopping intention changes with change in intention and sample size. i.e If two persons work on the same data and have different stopping intention, they may get two different  p- values for the same data, which is undesirable.

For example: Person A may choose to stop tossing a coin when the total count reaches 100 while B stops at 1000. For different sample sizes, we get different t-scores and different p-values. Similarly, intention to stop may change from fixed number of flips to total duration of flipping. In this case too, we are bound to get different p-values.





3.2 Bayes Theorem
Bayes Theorem comes into effect when multiple events form an exhaustive set with another event B. This could be understood with the help of the below diagram

https://www.analyticsvidhya.com/blog/2016/06/bayesian-statistics-beginners-simple-english/#h2_8


Since prior and posterior are both beliefs about the distribution of fairness of coin, intuition tells us that both should have the same mathematical form. Keep this in mind. We will come back to it again.

odels are the mathematical formulation of the observed events. Parameters are the factors in the models affecting the observed data. For example, in tossing a coin, fairness of coin may be defined as the parameter of coin denoted by θ. The outcome of the events may be denoted by D.


The reason that we chose prior belief is to obtain a beta distribution. This is because when we multiply it with a likelihood function, posterior distribution yields a form similar to the prior distribution which is much easier to relate to and understand.



选择一个先验，先验的解析形式，也后续决定了每次迭代的后验的表达式，当然中间条件概率的解析形式，也决定了后验朝着哪个解析形式去，到最后，条件概率更新，就是观察到这些数据，不再让先验和后验产生区别了，那我们的这个先验就已经包含了根据这个数据能得到的所有内容并尽量准确地描述了数据，才会这样
