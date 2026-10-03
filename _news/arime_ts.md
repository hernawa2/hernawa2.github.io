---
layout: default
title: Time-Series Analysis - Fundamentals
date: 2026-04-20
math: true
---
# Overview
Just like previous post, the goal of this blog post is to introduce the motivation and underlying fundamental concept of temporal analysis. I will use as few equations as possible to introduce the main concept I want to cover in this blog post.

# Problem Statement
Suppose you observe a sequential dataset (i.e., daily temperature or number of daily passenger) and we are tasked with finding a model (i.e., $f(x)$) that can describe the phenomena well (i.e., capture the mean at each time step). What would be the next rational step to follow?

# Our Mission
Any time-series data can be described as a sequence of random variable ($Y_t$ - the t here represents the time step, could be minute, months or days) taken across a particular time unit. There are two main goals of any time-series analysis:
1. Understanding the underlying data-generation distribution
2. Forecasting into the future
Depending on the goal of the analyst, there are analysis tools that can serve to aim both and other tools only serve one or the other. Regardless, once the underlying data-generation distribution has been determined, usually, the quality of forecasting becomes better too. However, we should very particular about the term "forecasting" since recently, it has been used interchangeably with extrapolation. To put it simply, merely doing extrapolation (we will discuss this later what this means) is not the same as doing proper forecasting.

# Types of Time-Series Process
Generally, any time-series data $Y_t$ can be described as either stationary or non-stationary, Gaussian (normal) or non-Gaussian and/or homoscedastic or heteroskedastic. We can define using simple terms each as following:

* **Stationary**: the mean and variance of $Y_t$ are constant and equal everywhere throughout the entire time-series.
* **Non-stationary**: mostly varying mean or varying variance throughout the entire time-series.
* **Gaussian**: each $Y_t$ follows a univariate Gaussian distribution. If we collect all $Y_t$, the underlying distribution is multivariate Gaussian random variable.
* **Non-Gaussian**: each $Y_t$ do not follow Gaussian distribution and often shows heavy-tails or sudden jump.
* **Homoscedastic**: the variance across time horizon remains constant.
* **Heteroskedastic**: the variance across time horizon is not constant.

Ok, I just introduced many technical terms but fret not, we shall discuss them in great details. So one might ask, ok, for every $Y_t$, say at $Y_1$, you only observe one value, then how do you determine if the time-series process at $Y_1$ follows a univariate Gaussian distribution?
I specifically leave out the discussion on autocovariance/covariance to simplify this blog post. Among

To be continued...
