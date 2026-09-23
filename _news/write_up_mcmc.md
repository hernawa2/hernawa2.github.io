---
layout: default
title: Fundamental of Markov Chain Monte Carlo
date: 2026-03-18
math: true
---

# Overview
The goal of this blog post is to introduce the motivation and concept of Markov Chain Monte Carlo for those without strong statistical or mathematical background. I will try my best to use as many as equations as possible and visualize the process instead.

# Problem Statement
Suppose there is a function (i.e., $f(x)$), parameterized by $\theta$ (in simple linear regression $y=mx+b$, this would be the $m$ and $b$), that has been judged to be suitable to fit/model some observed values. The goal is then how do we estimate the value(s) of $\theta$. The typical go-to solution would be an optimization $\theta$ relative to some pre-defined objective (usually minimization of error between the function and the observed values)


The fundamental concept of Markov Chain Monte Carlo (MCMC) is relatively simple.
