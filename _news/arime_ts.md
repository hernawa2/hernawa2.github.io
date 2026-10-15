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

# Types of Time-Series Process - Covering the Data-Generation Process
Generally, any time-series data $Y_t$ can be described as either stationary or non-stationary, Gaussian (normal) or non-Gaussian and/or homoscedastic or heteroskedastic. We can define using simple terms each as following:

* **Stationary**: the mean and variance of $Y_t$ are constant and equal everywhere throughout the entire time-series.
* **Non-stationary**: mostly varying mean or varying variance throughout the entire time-series.
* **Gaussian**: each $Y_t$ follows a univariate Gaussian distribution. If we collect all $Y_t$, the underlying distribution is multivariate Gaussian random variable.
* **Non-Gaussian**: each $Y_t$ do not follow Gaussian distribution and often shows heavy-tails or sudden jump.
* **Homoscedastic**: the variance across time horizon remains constant.
* **Heteroskedastic**: the variance across time horizon is not constant.

Ok, I just introduced many technical terms but fret not, we shall discuss them in great details. So you might ask, ok, for every $Y_t$, say at $Y_1$, you only observe one value, then how do you determine if the time-series process at $Y_1$ follows a univariate Gaussian distribution?

<img src="/assets/img/ts_example.png" alt="sample" width="750">

So, you might observe a time-series data that looks like the first plot above. Since we can look at time-series as a stochastic process, what happens when you can actually observe this quantity again under the exact same condition (like parallel world) and you collect all of the observation and plot them all together, then you might observe the second plot above. So what happens here is that, if we slice, collect, and plot data at, say in $t=1$, we will see that the distribution resembles a Gaussian distribution. This is what we mean when the time-series is Gaussian. Secondly, if we plot the histogram in 3D all of $Y_{t=1}$ and $Y_{t=20}$, then we will get a multivariate Gaussian distribution and this is true for any and all of the $Y_t$ above.

<img src="/assets/img/gauss_mult.png" alt="sample" width="750">

In the case above, we have a non-stationary Gaussian Homoscedastic time-series where the mean of the process can be modelled as a linear model with independent noise. If the covariance of the multivariate Gaussian is computed, we will have the same entry in the diagonal (since the variance is constant at each $t$) and values approximately zero at every other location in the matrix (in this case, the $Y_t$ is independent at every $t$). However, this is almost certainly not the case in real life, the noise can be correlated. I specifically leave out the discussion on autocovariance/covariance and the lag concept to simplify this blog post.

But of course, in real life, we only observe one **realization** just like shown in the first plot above and not the entire possibility across each $t$. This is the challenge in uncovering the data-generating process with only a single realization. Typically, the process to determine what kind of time series we are dealing with, the first approach is to do decomposition of the time-series to trend (mean), seasonality (if any), and residual (noise). For most of the time, modeling trend would be the first objective and is typically sufficient for most purpose. Modeling seasonality and residual would be more involved. One of the most popular approach is through [Seasonal-Trend decomposition using LOESS (STL)](https://www.math.unm.edu/~lil/Stat581/STL.pdf).

<img src="/assets/img/STL_res.PNG" alt="sample" width="750">

All of the steps above are some of the initial steps to uncover the data-generating distribution in a time-series process. Next, we will talk about a extrapolation/forecasting of time-series, which is what most people are more interested in.

# Forecasting = Extrapolation ?

We have come to the most fascinating section of the time-series analysis. Just like what I alluded previously, most of the time, extrapolation is simply predicting the conditional mean at time $t$ given past historical records. Forecasting (i.e., predicting the future) is then inherently probabilistic by nature. The same concept is actually also applied to weather forecasting. Briefly speaking, the mean of the probabilistic output should generally be the conditional mean of whatever extrapolation model that is used.

I will discuss both in greater details in subsequent post. But let us assume that we are satisfied that extrapolation is equal to forecasting. The next question is then, what model do we use? I would generally classify the modeling types into three: models that are intrinsically temporal, models that are not intrinsically temporal, and function-based model. 

Some examples of forecasting models that are intrinsically temporal are
* Autoregressive class models
* Recurrent-based Neural Network (e.g., LSTM, GRU)
* Transformers

Some people would use state estimation models such as Kalman Filter as intrinsically temporal. While true, I would not classify KF as a forecasting model in the strictest sense.

On the other hand, some examples of forecasting models that are not intrinsically temporal are
* Tree-based model (e.g., XGBoost, Random Forest)
* regression based model
* And many more

And function-based models include
* Gaussian process regression
* Spline

The main difference between the intrinsically temporal models and the ones who are not is the built-in temporal structure. I will discuss some autoregressive (AR) models later as an example but in AR models, the next value forecasted is a linear combination of the previous $K$ values. Therefore, there is a built-in temporal structure that constraints the model's forecasted value. Therefore, many classical statistical forecasting methods (i.e., AR) are univariate by design - although modifications can be made to accommodate multivariate and most neural network-based models can handle multi-input, single output scenario. 

On the other hand, regression based models require an explicit encoding of the temporal element in the input. This requires some feature engineering derived from the original time-series such as lag at 7 days, or lag at 31 days so on and so forth. Then, the model can identify underlying patterns between the actual time-series with its lagged values, therefore creating a temporal chain.
