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

Since the stochastic matrix only contains distinct words from the text, that means the words we are predicting are also only coming from this finite set of words. Even if we build a stochastic matrix from the entire collection of books, webpage, and articles that have ever been written, the set of words is still finite and therefore, our prediction would not be of some new, made-up word. To generate the subsequent word, we would go to the row that corresponds to the previous word, then we would do weighted sampling proportional to the relative frequency values along the row. After all, this is still a probabilistic model.

For example, a short snippet of the row from the stochastic matrix that corresponds to the word "i" is shown below

<img src="/assets/img/stoc_matrix_i.png" alt="sample_plot" width="750">

Note that there are many zeroes (i.e., sparse) within the matrix because from the limited text that we build the stochastic matrix on, we did not record any occurrences of the words 'i' followed by 'age' for example. The actual row is actually much longer with 4,679 entries (i.e., we counted 4,679 unique words in the text!). In fact, the entire stochastic matrix is of the size 4,679 by 4,679. Now, let's assume that we want to generate/predict what sentence we can create with the starting word 'i'. For simplicity, let us limit the length of the sentence to comprise of 7 words.

* First Realization: 'i' + 'have' + 'died' + 'for' + 'a' + 'candle' + 'too' + 'far'
* Second Realization: 'i' + 'really' + 'better' + 'hire' + 'a' + 'laugh' + 'she' + 'sir'
* Third Realization: 'i' + 'did' + 'just' + 'keep' + 'up' + 'kate' + 'often' + 'that'

From our little experiment above, it seems to be creating sentences that make sense if we limit the context to perhaps 4-5 words maximum. What we just demonstrated is also called a unigram language model. It is the most simplistic approach in generating text. An extension to this would be to reframe how we see Markov Chain. Earlier, we define that in Markov Chain, the probability of transitioning to a future state (i.e., $t+1$) only depends on the current state (i.e., $t); However, we can redefine what current state means. Instead of simply taking the state only at time $t$, we can formulate it that the current state is the previous 2 observed states ($t$ and $t-1$) or we can go further to previously 3 observed states, so on and so forth. Then, the stochastic matrix in a 2-gram model (i.e., $P(X_{t+1}|[X_t, X_{t-1}])$ - similar to the order parameter in autoregressive model), would have a pair of subsequent word that we can use to predict the next word. As such, for example, the 'i' word in the stochastic matrix, would be replaced with 'i advised', 'i told', and so on and so forth accordingly to the text, providing more context for our next-word prediction.

Nonetheless, now, imagine if we create the stochastic matrix based on the web database and any previously written materials, our text generation strategy would fail because any sentence creation would just seem to be a random collection of words that might make sense to humans but lacks any context/domain. This is where the deep learning model transformers comes into the picture. Transformer works great for 'large language modeling' because it is able to provide context through the Multi-Head Attention architecture built into the model. What this means is that, if we prompt (i.e., providing input) transformer model, instead of just relying on the previous word to make a prediction on the next one, it would instead also look at the entire prompt as a whole, identify keywords that are able to provide context, and constructed multiple weighting scheme on the next prediction. We can think about it in this way, imagine we have the full stochastic matrix of everything that we have written so far in the history of mankind, instead of selecting words from the row based only on relative frequency, transformer tells the predictor to only focus on specific sections of the column that actually is representative to the context of the initial prompt. That way, the next-word prediction would fall in context and generate text that make sense to us contextually.

# Other uses of Markov Chain
As we demonstrated above, Markov Chain provides a strong fundamental framework to model subsequent process in a surprisingly compact and simple form. Some areas that benefit from Markov Chain is wildfire propagation modeling, guidance of spaceship/rocket through Kalman Filter, and early-stage pandemic propagation modeling. These are but just a snippet of the list of practical application of Markov Chain and for that we need to thank the great [Andrey Markov](https://en.wikipedia.org/wiki/Andrey_Markov) himself.

