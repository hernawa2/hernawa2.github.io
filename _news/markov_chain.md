---
layout: default
title: Markov Chain - From the first statistical language model to Google's PageRank
date: 2026-07-26
math: true
---

# Overview
Markov Chain is, without a doubt, one of the most powerful framework to model random process. This blog will explore some of its features and perhaps, limitations, particularly in language modeling.

# Problem Statement
Suppose you have a frog that is trapped in a well and there are five light wooden blocks that the frog can land on. However, as soon as the frog lands on any one of the wooden blocks, it will start sinking so the frog will have to decide on which other wooden blocks to jump onto.
This is a classical example of a problem that can be solved easily using a Markov Chain.

# Discrete Markov Chain
For the purpose of discussion, we would consider discrete states (i.e., the five different countable wooden blocks) Markov Chain. Formally, a Markov Chain can be defined as $P(X_{t+1}|X_t)$. This simply states that the next state where I am going to be only depends on the previous state and nothing else.
For our example, this means that which wooden block the frog decided to jump to, only depends on its current wooden block is sitting on. All previously visited wooden blocks simply do not matter (i.e., memoryless frog). The illustration on how the problem above can be represented as a Markov Chain is shown below.

<img src="/assets/img/markov_chain.png" alt="sample_plot" width="750">

Then how does the frog know which wooden block to jump to? The probability of where the frog decides to jump to can be depicted with a transition/stochastic matrix.

<img src="/assets/img/stoc_matrix.png" alt="sample_plot" width="750">

The summation of every row has to sum to one. Therefore, when the frog is at Block 1, there are 10% chance that it remains in Block 1 (i.e., jumping vertically), 45% chance that it jumps to Block 2, 30% chance that it jumps to Block 3, and 15% chance it jumps to Block 4. The frog cannot jump to Block 5 from Block 1 directly die to the great distance. Then, similarly when the frog is at Block 2, the same analysis can be conducted.

Therefore, we can start asking questions such as "what is the expected first return time to Block 1?". We can simulate this very easily or theoretically compute the expected return time. The practical application of this is on network and internet applications to predict traffic flow. Furthermore, Google's PageRank (i.e., the list of websites ranked from search) was also modeled with Markov Chain and achieved superior results compared to at the time its competitor Yahoo. Now, let us discuss a simple language model based on the Markov Chain.


### Simple Language Model
Let us switch the state from wooden blocks to words. Essentially, we are asking, if my current word is "arrived", what is the likely subsequent word? Let us consider the text [Twilight: A Story of Two Villages](https://www.gutenberg.org/cache/epub/79755/pg79755-images.html) To compose the stochastic matrix, first, we turn all of the words to lowercase, remove any punctuations, and exclude all of the non-content text. Then, we identify only the distinct word $n$ and create a $n$ by $n$ stochastic matrix. For each unique word, we find all of its location on the main text and identify all of the next words for each occurrence of the unique word. This way, we can populate the stochastic matrix by its relative frequency of each unique word and we are ready to generate our text from the context of the main text.

Generation of text

So, all method that included the name "Bayesian" such as Bayesian Neural Network or Bayesian Linear Regression, are just a modified version of its original optimization counterpart. Instead of optimization, they employ MCMC-adjacent sampling to retrieve the posterior distribution.

Hopefully, this blog post helps to understand the motivation and main concept of MCMC. Next, I will post about Hamiltonian Monte Carlo and how Hamiltonian dynamics help choose a better new point (instead of randomly walking!)

