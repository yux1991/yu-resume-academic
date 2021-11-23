---
title: Chapter 1
linktitle: Introduction
type: book
summary: Introduction to NLP and word vectors.

# Date published
date: "2021-11-17T00:00:00Z"

featured: false

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
    * The matrix $X$ stores co-occurrences of words thereby becoming an affinity matrix.
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
* **Continuous Bag of Words Model (CBOW)**
  * General idea:
    * Predicting a center word from the surrounding context
    * For each word, learn 2 vectors:
      * $v$: (input vector) when the word is in the context
      * $u$: (output vector) when the word is in the center
  * Notation for CBOW model:
    * $w_i$ : word $i$ from vocabulary $V$.
    * $\mathcal{V}\in\mathbb{R}^{n\times|V|}$ : input word matrix
    * $v_i$ : $i$-th column of $\mathcal{V}$, the input vector representation of word $w_i$.
    * $\mathcal{U}\in\mathbb{R}^{|V|\times n}$ : output word matrix
    * $u_i$ : $i$-th row of $\mathcal{U}$, the output vector representation of word $w_i$.
  * CBOW steps:
    1. Generate one-hot word vectors for the input context of size $m$: $(x^{(c-m)},\cdots,x^{(c-1)},x^{(c+1)},\cdots,x^{(c+m)}\in\mathbb{R}^{|V|})$.
    2. Get the embedded word vectors for the context $(v\_{c-m}=\mathcal{V}x^{(c-m)}, v\_{c-m+1}=\mathcal{V}x^{(c-m+1)},\cdots,v\_{c+m}=\mathcal{V}x^{(c+m)}\in\mathbb{R}^n)$.
    3. Average these vectors to get $\hat{v}=\frac{v\_{c-m}+v\_{c-m+1}+\cdots+v\_{c+m}}{2m}\in\mathbb{R}^n$.
    4. Generage a score vector $z=\mathcal{U}\hat{v}\in\mathbb{R}^{|V|}$.
    5. Turn the scores into probabilities $\hat{y}=\operatorname{softmax}(z)\in\mathbb{R}^{|V|}$.
    6. Minimize the cross entropy $H(\hat{y},y)$ between the predicted probability distribution $\hat{y}$ and the true probability distribution $y$:
    $$
      H(\hat{y},y)=-\sum\_{j=1}^{|V|}y\_i\operatorname{log}(\hat{y}\_i)=-y\_i\operatorname{log}(\hat{y}\_i)
    $$
    7. Optimization objective:
    $$
      \operatorname{minimize}\ J=-\operatorname{log}\ P(w\_c|w\_{c-m},\cdots,w\_{c-1},w\_{c+1},\cdots,w\_{c+m})
    $$

    $$
      =-\operatorname{log}\ P(u\_c|\hat{v})
    $$

    $$
      =-\operatorname{log}\frac{\exp(u\_c^T\hat{v})}{\sum\_{j=1}^{|V|}\exp(u\_j^T\hat{v})}
    $$

    $$
      =-u\_c^T\hat{v}+\operatorname{log}\sum\_{j=1}^{|V|}\exp(u\_j^T\hat{v})
    $$
  * How CBOW works?
 {{< figure src="cbow.png" caption="Figure 1. CBOW" theme="light" >}} 
* **Skip-Gram Model**
  * General idea:
    * Predicting surrounding contex words given a center word.
  * Notation for Skip-Gram model:
    * $w_i$ : word $i$ from vocabulary $V$.
    * $\mathcal{V}\in\mathbb{R}^{n\times|V|}$ : input word matrix
    * $v_i$ : $i$-th column of $\mathcal{V}$, the input vector representation of word $w_i$.
    * $\mathcal{U}\in\mathbb{R}^{|V|\times n}$ : output word matrix
    * $u_i$ : $i$-th row of $\mathcal{U}$, the output vector representation of word $w_i$.
  *  Skip-Gram steps:
    1. Generate one-hot input vectors $x\in\mathbb{R}^{|V|}$ of the center word.
    2. Get embedded word vector for the center word $v_c=\mathcal{V}x\in\mathbb{R}^n$.
    3. Generate a score vector $z=\mathcal{U}v_c$.
    4. Turn the scores into probabilities $\hat{y}=\operatorname{softmax}(z)\in\mathbb{R}^{|V|}$.
    5. Match the predicted probability $\hat{y}$ to the true probability $y$.
    6. Naive Bayes assumption: given the center word, all output words are completely independent.
    7. Optimization objective:
    $$
      \operatorname{minimize}\ J=-\operatorname{log}\ P(w\\_{c-m},\cdots,w\\_{c-1},w\\_{c+1},\cdots,w\\_{c+m}|w\\_c)
    $$

    $$
      =-\operatorname{log}\prod\_{j=0,j\neq m}^{2m}P(w\_{c-m+j}|w\_c)=\sum\_{j=0,j\neq m}^{2m}\ H(\hat{y},y\_{c-m+j})
    $$

    $$
      =-\operatorname{log}\prod\_{j=0,j\neq m}^{2m}\frac{\exp(v\_{c-m+j}^Tv\_c)}{\sum\_{k=1}^{|V|}\exp(u\_k^Tv\_c)}
    $$

    $$
      =-\sum\_{j=0,j\neq m}^{2m}\ u\_{c-m+j}^Tv\_c+2m\operatorname{log}\sum\_{k=1}^{|V|}\exp(u\_k^Tv\_c)
    $$
  * How Skip-Gram works?
 {{< figure src="skipgram.png" caption="Figure 2. Skip-Gram" theme="light" >}} 
