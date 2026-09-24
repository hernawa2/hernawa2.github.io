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
The question that MCMC tries to answer is relatively simple: given the observed quantities above, can I estimate the variation of the mean at a given condition. Therefore, to estimate the variation of the mean, $\theta$ must have some distribution that we can sampled from since the behavior of $f(x)$ is dictated by the $\theta$ used. The challenge is how do we estimate this distribution (i.e., posterior) of which we can sample $\theta$ from. It is also important to note that MCMC does not try to capture the entire inherent randomness of the process (modeling entire randomness of a certain process is called stochastic modeling).

Formally, MCMC is the meat-and-potato of **Bayesian inference** to sample from complex distribution with no closed-form solution. Side note: a closed-form known distribution would be a Gaussian/normal distribution with known mean and standard deviation.

There are essentially two main goals of MCMC:
1. To estimate the mean of the process (similar to the optimization procedure),
2. To estimate the correlation between each of the parameter set $\theta$

As with any Bayesian inference process, we need two ingredients: the prior and the likelihood.

### Prior information
Before exploring MCMC further, we need to understand what prior information is. A simple example would be when you are visiting a new city and looking up for a place to eat. Most people would open google map or yelp to look for options and look for the highly rated restaurant. Subsequently, you might even spend some more time looking at the reviews, menu and potentially pictures of dishes online before deciding on which restaurant to go to. This is known as our *a priori* (prior information), our state of knowledge before observing any quantities of interest; in this case, it would be how the dish actually tastes. Prior information can take many shapes and form, this also includes a prior information where we know nothing about the restaurant around and simply walk in to any place for a quick meal.

Formally, the prior information should contain any knowledge on the parameter set $\theta$ we would have before observing the quantity of interest (in this example, tasting the dish). Typically, a **Probability Density Function** (PDF) is prescribed as prior information. Therefore, A *strong* prior could mean a normal distribution of some mean and relatively small standard deviation. On the other hand, a *weak* prior could mean a uniform distribution over some range.

### The Likelihood
In layman terms, the likelihood measures how far are the $f(x)$ (from here on out, I am going to call this the *model prediction* at $x$) from the observed quantities. Since MCMC is a sampling technique, every time we take a sample of $\theta$, there has to be a mechanism to determine if $\theta$ produces model prediction that are close to the observed quantities, and that is precisely what the likelihood is for.

The mechanics itself is quite straightforward where the likelihood function is prescribed to be some kind of PDF that can describe the error or residual distribution of the process. For example, given a set of $x$, and that the underlying process is a [[Gaussian Process]](https://en.wikipedia.org/wiki/Gaussian_process) 
