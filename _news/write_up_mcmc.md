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

### The Likelihood function
In layman terms, the likelihood measures how far are the $f(x)$ (from here on out, I am going to call this the *model prediction* at $x$) from the observed quantities. Since MCMC is a sampling technique, every time we take a sample of $\theta$, there has to be a mechanism to determine if $\theta$ produces model prediction that are close to the observed quantities, and that is precisely what the likelihood is for.

The mechanics itself is quite straightforward where the likelihood function is prescribed to be some kind of PDF that can describe the error or residual distribution of the process. For example, given a set of $x$, and that the underlying process is a [Gaussian Process](https://en.wikipedia.org/wiki/Gaussian_process), an appropriate likelihood function is a Multivariate Normal Distribution with a vector mean of the observed quantity and a covariance function built using the observed quantity. Once both prior information and likelihood function has been defined, we are then ready to proceed with the sampling procedure

## Optimization
To appreciate what MCMC actually does, it is always a good exercise to formulate the same problem from the optimization point of view. 
<img src="/assets/img/sample.png" alt="sample" width="750">
Consider the figure above. We think that the function $y = Ie^{-cx}$ with parameter $I$ and $c$ can satisfactorily described (or fit) the observation above. If we just plug in a random guess of $I=1.5$ and $c=-0.8$, then we get the black curve below. Qualitatively, it is quite good but what if we optimize it with respect to the quantity $y$? we do this by specifying what we want to minimize and in this case, we can use the average squared distance between each point to the line. Sidenote: we used squared distance to remove the negative sign.

<img src="/assets/img/sample_plot.png" alt="sample_plot" width="750">

The video below shows how an optimization (using gradient descend - I will talk about optimization in another post) procedure is conducted. The X-axis represents the parameter $I$ and the Y-axis represents the parameter $c$ and moreover, the background of the figure illustrates the averaged square distance or the error/loss. The objective is to then move to a point where the combination of $I$ and $c$ shows the lowest averaged square distance.

<video width="800" height="600" controls>
  <source src="/assets/img/opt.mp4" type="video/mp4">
</video>

Since now we have a point of $I$ and $c$ where the averaged square distance at its lowest, we then use this value of $I$ and $c$ to replot the blue line. If the goal is to estimate the mean of the process using $y = Ie^{-cx}$, then our job is done.

<img src="/assets/img/sample_opt.png" alt="sample_opt" width="750">

## The Mechanics of Sampling
Imagine that you have had too much to drink and it's late at night, you are trying to go home but your senses are impaired and you cannot make sound judgement. However, you have a lot of time to figure out the home location. You also know that your house is by the train station, so the nearer you are, the more likely you are going to hear a train passing by (let's assume that there is an infinitely long train that is currently passing through the train station near your home). 

Starting from the bar, since you do not know where to go (unguided), you pick a random direction, and you go there. Now at this new location, you assess and listen carefully if you hear train passing, if the sound gets louder compared to the original spot you came from, then you move to this new location. Then at this new location, again, because you do not know where to go, you again pick a random direction to go - this phenomena is called [Random Walk](https://en.wikipedia.org/wiki/Random_walk). At this new location, however, the train sound is actually more distant, so you go back to your previous location. At the previous location, again, pick a random direction to go. At this new location, the train sound is actually more quite and you are actually further from your target compared to the previous location, but, since your senses are impaired, you decided to go to this new location. This is where the name Markov Chain Monte Carlo comes from. Markov Chain denotes that you are only comparing the train noise between your new location and previous location, and do not consider any other travelled points previously. Furthermore, the walking in random direction every time you move to a new point is where the Monte Carlo naming comes from. If you repeat this process multiple times, you are then guaranteed at one point, that you will reach your target. But once you are near your target, it is not possible for you to exactly determine the location of your exact house (even if you are standing in front of it) because your senses are extremely impaired!


<img src="/assets/img/drunk_man.png" alt="drunk_man" width="750">


Back to the original observations above, we justified that the model $y = Ie^{-cx}$ is sufficient in describing the observation. Now, using the logic above, we start with a random point for both $I$ and $c$. The drunk man is now $I$ and $c$ and the house is now your *posterior* distribution (sometimes also called target distribution). Then, the distance between the model prediction and the observation now symbolizes the intensity of the train sound. Lastly, not covered above, the drunk man's subconscious awareness is now the prior. The process of MCMC sampling is shown below in the space of $I$ and $c$.

<video width="800" height="600" controls>
  <source src="/assets/img/mcmc.mp4" type="video/mp4">
</video>

If you watch the entire video above, you will soon realize that the sampling had reached its posterior distribution. If we plot how frequent each point is visited, we, then get the full posterior *joint* distribution of $I$ and $c$. Do you notice anything special?

That is it for MCMC. The example I show above is pedagogical and real-application is, more-often than not, always more complex. In high-dimension problem (the number of parameters $\theta$ is a lot), MCMC may take a very long time to reach the posterior distribution. If you ponder about it, in two-dimensional space, walking randomly will almost surely get you to where you want to go. But in dimension higher than that, unguided random walk stretches where the new point is, one parameter might want to go to the left, others go to the right, while other parameters want to go up to reach the target.

There are of course, other modified version of MCMC such as Multiple-Try Metropolis, Adaptive MCMC, Langenvin Monte Carlo, and Hamiltonian Monte Carlo. There is even other non-computational method to compute the posterior distribution such as Variational Inference but I will cover this in another blog post.

So, all method that included the name "Bayesian" such as Bayesian Neural Network or Bayesian Linear Regression, are just a modified version of its original optimization counterpart. Instead of optimization, they employ MCMC-adjacent sampling to retrieve the posterior distribution.

Hopefully, this blog post helps to understand the motivation and main concept of MCMC. Next, I will post about Hamiltonian Monte Carlo and how Hamiltonian dynamics help choose a better new point (instead of randomly walking!)
