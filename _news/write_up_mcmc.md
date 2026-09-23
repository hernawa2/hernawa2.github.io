---
layout: default
title: Fundamental of Markov Chain Monte Carlo
date: 2026-03-18
math: true
---

# Overview
The goal of this blog post is to introduce the motivation and concept of **Markov Chain Monte Carlo** (MCMC) for those without strong statistical background. I will try my best to use as little equations as possible and visualize the process instead.

# Problem Statement
Suppose there is a function (i.e., $f(x)$), parameterized by $\theta$ (in simple linear regression $f(x)=mx+b$, this would be the $m$ and $b$), that has been judged to be suitable to fit/model some observed quantities. The goal is then how do we estimate the value(s) of $\theta$. The typical go-to solution would be an optimization $\theta$ relative to some pre-defined objective (usually minimization of error between the function and the observed values).

True with any processes in our world, there is an inherent randomness within the quantity that we are interested in measuring (daily temperature or number of churning customers in an online platform). The randomness itself can come from nature or how we collect/sample the quantity that we are interested in. An optimization procedure above would try to estimate the mean or expected value of the quantity measured at a given condition. This means that optimization does not incorporate any randomness into the estimated mean.

# Markov Chain Monte Carlo
The question that MCMC tries to answer is relatively simple: given the observed quantities above, can I estimate the variation of the mean at a given condition. It is important to note that MCMC does not try to capture the entire inherent randomness of the process (modeling entire randomness of a certain process is called stochastic modeling).

Formally, MCMC is the meat-and-potato of **Bayesian inference** to sample from complex distribution with no closed-form solution. Side note: a closed-form known distribution would be a Gaussian/normal distribution.

Before deciding on There are two main goals of MCMC
As with any Bayesian inference process, 
