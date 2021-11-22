---
title: Chapter 1
linktitle: Introduction
type: book
summary: Introduction to NLP and word vectors.

# Date published
date: "2021-11-17T00:00:00Z"

featured: false
image:
  caption: 'Image credit: [**International Banker**](https://internationalbanker.com/technology/how-the-financial-industry-is-using-natural-language-processing/)'
  focal_point: ""
  placement: 2

authors:
- admin

tags:
- NLP
- Word Vectors
- Singular Value Decomposition
- Skip-gram
- Continuous Bag of Words(CBOW)
- Negative Sampling
- Hierarchical Softmax
- Word2Vec

weight: 1

categories:
- Course Notes

---
## 1. Introduction

### What are the common NLP tasks?

* Easy
  * Spell Checking
  * Keyword Search
  * Finding Synonyms
* Medium
  * Parsing information from websites, documents, etc.
* Hard
  * Machine Translation (e.g. Translate Chinese text to English)
  * Semantic Analysis (What is the meaning of query statement?)
  * Coreference (e.g. What does "he" or "it" refer to given a document?)
  * Question Answering (e.g. Answering Jeopardy questions).

## 2. Word Vectors

### One-hot vector

* Represent every word as an $\mathbb{R}^{|V|\times1}$ vector with all 0s and one 1 at the index of that word in the sorted english language, where $|V|$ is the size of the vocabulary.
* This word representation does not give us directly any notion of similarity because all the vectors are orthogonal.

### SVD based methods

* General idea:
  * Loop over a massive dataset and accumulate word co-occurrence counts in some form of a matrix $X$.
  * Perform SVD on $X$ to get $USV^T$ decomposition.
  * Use the rows of $U$ as the word embeddings for all words in our dictionary.
* Choices of $X$:
  * Word-Document Matrix: 
    * Assumption: words that are related will often appear in the same documents.
    * Loop over all documents and for each time word $i$ appears in document $j$, we add one to entry $X_{ij}$.
  * Window based Co-occurrence Matrix:
    * The matrix $X$ stores co-occurrences of words theereby becoming an affinity matrix.
    * Calculate the number of times each word appears inside a window of a particular size around the word of interest.
* Applying SVD to the cooccurrence matrix
  * Apply SVD on $X$ to get $X=USV^T$.
  * Select the firs $k$ columns of $U$ to get $k$-dimensional word vectors.
  * $\frac{\sum_{i=1}^k\sigma_i}{\sum_{i=1}^{|V|}\sigma_i}$ indicates the amount of variance captuered by the first $k$ dimensions.
* Problems with the SVD based methods
  * SVD based methods do not scale well for big matrices.
  * It is hard to incorporate new words or documents.
  * Computational cost for a $m\times n$ matrix is $O(mn^2)$.

### Iteration Based Methods - Word2vec

* General idea:
  * Design a model whose parameters are the word vectors
  * Train the model on a certain objective.
  * Learn the word vectors with "backpropagating".
* Work2vec:
  * 2 algorithms:
    * Continuous bag-of-words (CBOW): predict the center word from the surrounding context in terms of word vectors.
    * Skip-gram: predict the distribution (probability) of contex words from a center word.
  * 2 training methods:
    * Negative sampling.
    * Hierarchical softmax.
* Language Models:
  * Definition: models that assign probabilities to a sequence of words are called language models. Mathematically, we can represent this probability by:
  $$
    P(w_1, w_2, \cdots, w_n)
  $$
  * Unigram model:
  $$
    P(w_1, w_2, \cdots, w_n) = \prod_{i=1}^n P(w_i)
  $$
  * Bigram model:
  $$
    P(w_1, w_2, \cdots, w_n) = \prod_{i=2}^n P(w_i|w_{i-1})
  $$
  * N-gram model:
  $$
    P(w_1, w_2, \cdots, w_n) = \prod_{i=N-1}^n P(w_i|w_{i-N+1:i-1})
  $$
* Continuous Bag of Words Model (CBOW)
  * 