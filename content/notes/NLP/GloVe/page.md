---
title: Chapter 2
linktitle: GloVe, Evaluation and Training
type: book
summary: Word Vectors part II - GloVe, Evaluation and Training.

# Date published
date: "2021-11-17T00:00:00Z"

featured: false

authors:
- admin

tags:
- CS224n
- NLP
- GloVe

weight: 2

categories:
- Course Notes

---
## 1. Introduction

### Previous Methods

* Matrix Factorization Methods
  * Examples:
    * Latent semantic analysis (LSA)
    * Hyperspace analogue to language (HAL)
  * General idea:
    * These methods utilize low-rank approximations to decompose large matrices that capture statistical information about a corpus.
    * In LSA, the matrices are of “term-document” type.
    * In HAL, the matrices are of "term-term" type.
  * Pros:
    * Efficiently leverage statistical information.
  * Cons:
    * Perform relatively poorly on the word analogy task, indicating a sub-optimal vector space structure.

* Shallow Window-Based Methods
  * Examples:
    * Skip-gram
    * CBOW
  * General idea:
    * In skip-gram, the objective is to predict a word’s context given the word itself.
    * In CBOW, the objective is to predict a word given its context. 
  * Pros:
    * Through evaluation on a word analogy task, these models demonstrated the capacity to learn linguistic patterns as linear relationships between the word vectors.
  * Cons:
    * They do not operate directly on the co-occurrence statistics of the corpus.
    * Fails to take advantage of the vast amount of repetition in the data.

### Global Vectors for Word Representation (GloVe)

* Introduction:
  * GloVe consists of a weighted least squares model that trains on global word-word co-occurrence counts and thus makes efficient use of statistics. 
  * The model produces a word vector space with meaningful sub-structure. 
  * It shows state-of-the-art performance on the word analogy task, and outperforms other current methods on several word similarity tasks
* Co-occurrence Matrix:
  * $X$: word-word co-occurrence matrix.
  * $X_{ij}$: number of times word $j$ occurs in the context of word $i$.
  * $X_i=\sum_{k} X_{ik}$: the number of times any word $k$ appears in the context of word $i$.
  * $P_{ij}=P(w_j|w_i)=\frac{X_{ij}}{x_i}$: the probability of $j$ appearing in the context of word $i$.
* Least Squares Objective
  * Recall that for skip-gram model, we use softmax to compute the probability of word $j$ appears in the context of word $i$:
    $$
        Q_{ij}=\frac{\exp{\overrightarrow{u}_j^T\overrightarrow{v}_i}}{\sum_{w=1}^W \exp{\overrightarrow{u}_w^T\overrightarrow{v}_i}}
    $$
  * The global cross-entropy loss can be calculated as:
    $$
        J=-\sum_{i\in corpus}\sum_{i\in context(i)}\log{Q_{ij}}
    $$
  * Because the same words $i$ and $j$ can appear multiple times in the corpus, it is more efficient to first group togetehr the same values for $i$ and $j$:
    $$
        J=-\sum_{i=1}^W\sum_{j=1}^WX_{ij}\log{Q_{ij}}
    $$
  * Recalling the notations $X_i=\sum_{k}X_{ik}$ and $P_{ij}=X_{ij}/X_i$, then:
    $$
        J=-\sum_{i=1}^WX_i\sum_{j=1}^WP_{ij}\log{Q_{ij}}=\sum_{i=1}^WX_iH(P_i,Q_i)
    $$
    where $H(P_i,Q_i)$ is the cross entropy of the distributions $P_i$ and $Q_i$.
  * The problems with cross-entropy loss:
    * It has the unfortunate property that distributions with long tails are often modeled poorly with too much weight given to the unlikely events. 
    * for the measure to be bounded it requires that the model distribution $Q$ to be properly normalized. This presents a computatonal bottleneck owing to the sum over the whole vocabulary.
  * Square loss is a good aternative because the normalization factors in $Q$ and $P$ are discarded:
    $$
        \hat{J}=\sum_{i=1}^W\sum_{j=1}^WX_{i}(\hat{P}_{ij}-\hat{Q}_{ij})^2
    $$
    where $\hat{P}_{ij}=X_{ij}$ and $\hat{P}_{ij}=\exp{\overrightarrow{u}_j^T\overrightarrow{v}_i}$ are the unnormalized distributions.
  * In order to solve the problem that $X_{ij}$ takes very large values, an effective remedy is to minimize the squared error of the logarithms of $\hat{P}$ and $\hat{Q}$:
    $$
        \hat{J}=\sum_{i=1}^W\sum_{j=1}^WX_{i}(\log{(\hat{P}_{ij})}-\log{(\hat{Q}_{ij})})^2
    $$

    $$
        =\sum_{i=1}^W\sum_{j=1}^WX_{i}(\overrightarrow{u}_j^T\overrightarrow{v}_i-\log{X_{ij}})^2
    $$
  * Finally, the weighting factor $X_i$ is not guaranteed to be optimal. Instead, we introduce a more general weighting function $f$:
    $$
        =\sum_{i=1}^W\sum_{j=1}^Wf(X_{i})(\overrightarrow{u}_j^T\overrightarrow{v}_i-\log{X_{ij}})^2
    $$
  *  One class of weighting functions that works well can be parameterized as:
    $$
        f(x)=
        \begin{cases}
        (x/x_{max})^\alpha & \quad \text{if} x<x_{max}\\\\
        1 & \quad \text{otherwise}\\
        \end{cases}
    $$
* Conclusion
  * the GloVe model efficiently leverages global statistical information by training only on the nonzero elements in a wordword co-occurrence matrix, and produces a vector space with meaningful sub-structure. 
  * It consistently outperforms word2vec on the word analogy task, given the same corpus, vocabulary, window size, and training time. 
  * It achieves better results faster, and also obtains the best results irrespective of speed.
