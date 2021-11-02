---
title: Gaussian Mixture Model
subtitle: A review of the Gaussian Mixture Model (GMM) and the Expectation–Maximization (EM) algorithm.

# Summary for listings and search engines
summary: A Gaussian mixture model is a probabilistic model that assumes all the data points are generated from a mixture of a finite number of Gaussian distributions with unknown parameters.

# Link this post with a project
projects: []

# Date published
date: "2021-11-01T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Scikit-learn**](https://scikit-learn.org/stable/auto_examples/mixture/plot_gmm_pdf.html)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Machine Learning


categories:
- Review

---
### Introduction

#### What is Gaussian Mixture Model?
The Gaussian mixture model has the form:
$$
  f(x)=\sum_{m=1}^M\alpha_m\phi(x;\mu_m,\Sigma_m),
$$
with mixing proportions $\alpha_m$, $\Sigma_m\alpha_m=1$, and each Gaussian density has a mean $\mu_m$ and covariance matrix $\Sigma_m$. One can think of mixture models as generalizing k-means clustering to incorporate information about the covariance structure of the data as well as the centers of the latent Gaussians.

### Overview

* Gaussian Mixture Model Parameters ($k$ Components): 
  * Clustering probabilities: 
    $$ 𝜋=(𝜋_1,⋯,𝜋_k). $$
  * Cluster means: 
    $$ 𝜇=(𝜇_1,⋯,𝜇_k). $$
  * Cluster covariance matrices: 
    $$ Σ=(Σ_1,⋯,Σ_k). $$
 
* Joint Distribution: 

  $$ p(x,z)=p(z)p(x∣z)=𝜋_z𝒩(x∣𝜇_z,Σ_z). $$
 
  * Notes: 
    * $x|z$ has distribution $𝒩(𝜇_z,Σ_z)$. $z$ corresponds to ($x$ is the true cluster assignment). 
    * Suppose we know the model parameters $𝜋_z$, $𝜇_z$, $Σ_z$, then it is easy to evaluate the join density $p(x,z)$. 

* Latent Variable Model: 
  * A latent variable model is a probability model for which certain variables are never observed. 
  * In the Gaussian mixture model, we don't observe $z$ (the cluster assignment). Therefore $z$ is a latent variable, or a hidden variable. 

### The GMM "Inference" Problem

* Suppose we observe $x$, we want to know its cluster assignment $z$. 
* The conditional probability for cluster $z$ given $x$ is: 
$$
  p(z∣x)=p(x,y)p(x).
$$

* The conditional distribution is a soft assignment to clusters. 

* A hard assignment is: 
$$
  z^∗=argmax_{z∈\{1,⋯,k\}}p(z∣x).
$$

* If we have the model, the inference is trivial. 

### Mixture Models: 

* Margin Distribution: 
  * The margin distribution for a single observation $x$ is: 
$$
  p(x)=∑_{z=1}^k p(x,z)=∑_{z=1}^k 𝜋_z𝒩(x∣𝜇_z,Σ_z).
$$

  * Notes: 
    * $p(x)$ is a convex combination of probability densities. 

* Mixture Distributions (or Mixture Models): 
  * A probability density $p(x)$ represents a mixture distribution or mixture model, if we can write it as a convex combination of probability densities. That is: 
$$
  p(x)=Σ_{i=1}^k w_ip_i(x),
$$ 

where $w_i≥0$, $Σ_{i=1}^k w_i=1$, and each $pi$ is a probability density. 

  * Notes: 
    * In the GMM, $x$ has a mixture distribution. 
    * More constructively, let $S$ be a set of probability distributions: 
      * Choose a distribution randomly from $S$. 
      * Sample $x$ from the chosen distribution. 
      * Then $x$ has a mixture distribution. 

### The GMM "Learning" Problem: 

* Statement of the problem: Given data $x_1,⋯,x_n$ drawn from a GMM. Estimate the parameters $𝜋_z$, $𝜇_z$, $Σ_z$. 
* Review: Estimating a Gaussian Distribution: 
  * The density for $x∼𝒩(𝜇,Σ)$ is: 
$$
  p(x∣𝜇,Σ)=\frac{1}{\sqrt{|2𝜋Σ|}}\exp{−1/2(x−𝜇)^TΣ^{−1}(x−𝜇)}.
$$

  * The log-density is: 
$$
  log p(x∣𝜇,Σ)=−1/2log|2𝜋Σ|−1/2(x−𝜇)^TΣ^{−1}(x−𝜇).
$$

  * The log joint density from a sample $x_1,⋯,x_n$ i.i.d. from a $𝒩(𝜇,Σ)$ distribution is: 

  $$
    J(𝜇,Σ)=∑_{i=1}^n log p(x∣𝜇,Σ)
  $$
  $$
    =−n/2log|2𝜋Σ|−1/2∑_{i=1}^n(x−𝜇)^T𝛴^{−1}(x−𝜇).
  $$

  * To estimate $𝜇$ and $Σ$ from a sample $x_1,⋯,x_n$ i.i.d. from a $𝒩(𝜇,Σ)$ distribution, we need to maximize the log joint density: 

  $$
    ∇_𝜇J(𝜇,Σ)=0⟹\hat{𝜇}_{MLE}
  $$
  
  $$
    =1/n∑_{i=1}^n x_i.
  $$
  
  $$
    ∇_ΣJ(𝜇,Σ)=0⟹\hat{Σ}_{MLE}
  $$
  
  $$
    =1/n∑_{i=1}^n (x_i−\hat{𝜇}_{MLE})^T(x_i−\hat{𝜇}_{MLE}).
  $$

* Estimating the GMM using maximum likelihood: 

  * Find parameter values with highest likelihood for the observed data. 
  * The model likelihood for $𝒟=(x_1,⋯,x_n)$ sampled i.i.d. from a GMM is: 

  $$
    L(𝜋,𝜇,Σ)=∏_{i=1}^n p(x_i)
  $$
  $$
    =∏_{i=1}^n ∏_{z=1}^k 𝜋_z𝒩(x_i∣𝜇_z,Σ_z).
  $$

  * The objective function is: 

  $$
    J(𝜋,𝜇,Σ)=∑_{i=1}^nlog\{∑_{z=1}^k𝜋_z𝒩(x_i∣𝜇_z,Σ_z)\}.
  $$ 

  * Plugging in the probability density for $𝒩(𝜇,Σ)$, we get the GMM log-likelihood:

  $$
    J(𝜋,𝜇,Σ)=
  $$
  $$
    ∑_{i=1}^n log∑_{z=1}^k \frac{𝜋_z}{\sqrt{∣2𝜋Σ_z∣}} \exp{−1/2(x−𝜇_z)^TΣ^{−1}(x−𝜇_z)}.
  $$
  

  * Issues with MLE for GMM: 
    * No closed form expression for MLE. 
    * There are $k!$ equivalent solutions. 
    * The likelihood goes to infinity as $𝜎^2⟶0$ for some outliers. 
      * Keep restarting optimization. 
      * Bayesian approach. 
    * Running SGD on the GMM log-likelihood objective can be done in principle, but is challenging. 

### The EM Algorithm for GMM: 

* Estimating a Fully-Observed GMM: 
  * Suppose we observe $(x_1,z_1),⋯(x_n,z_n)$ i.i.d. from GMM $p(x,z)$. Then find MLE is easy: 

  $$
    n_z=∑_i^n=1(z_i=z),
    \hat{𝜋}(z)=n_z/n.
  $$

  $$
    \hat{\mu}_z=1/n_z
  $$
  
  $$\times\Sigma_{i:z_i=z}x_i.$$

  $$
    \hat{\Sigma}_z=1/n_z
  $$
  
  $$\times\Sigma_{i:z_i=z}(x_i−\hat{\mu}_z)(x_i−\hat{\mu}_z)^T.$$

* Cluster Responsibilities: 
  * Denote the probability that observed value $xi$ comes from cluster $j$ by: 

  $$
    𝛾_i^j=p(z=j∣x=x_i),
  $$

which is the responsibility that cluster $j$ takes for observation $x_i$. 

  * Given the parameters $𝜋_z,𝜇_z,Σ_z$, it is easy to find: 

  $$
    𝛾_i^j=p(z=j∣x_i)
  $$
  $$
    =p(z=j,x_i)p(x_i)
  $$
  $$
    =𝜋_j𝒩(x_i∣𝜇_j,Σ_j)∑_{c=1}^k 𝜋_c𝒩(x_i∣𝜇_c,Σ_c).
  $$

  * The vector $(𝛾_i^1,⋯,𝛾_i^k)$ is exactly the soft assignment for $x_i$. 

* Algorithm
> * **Algorithm: EM algorithm for GMM** 
>  ---
>    * **Input**: 
>      * $𝒟={x_1,⋯,x_n}⊂𝒳$. 
>      * GMM ($k$ components): 
>   
>   $$
>     𝜋=(𝜋_1,⋯𝜋_k),
>   $$
>   $$
>     𝜇=(𝜇_1,⋯,𝜇_k),
>   $$
>   $$
>     Σ=(Σ_1,⋯,Σ_k).
>   $$ 
>
>    * **Initialize**: 
>  $$
>    𝜋(0),𝜇(0),Σ(0),t=0.
>  $$ 
>
>    * **While not converge**: 
>      * For $i=1,⋯,n$ and $j=1,⋯,k$: 
>   $$
>     𝛾_i^j=\frac{𝜋_j^{(t)}𝒩(x_i∣𝜇_j^{(t)},Σ_j^{(t)})}{∑_{c=1}^k𝜋_c𝒩(x_i∣𝜇_c,Σ_c)}
>   $$ // the "E step 
>
>      * For $c=1,⋯,k$: // the "M step 
>   
>   $$
>     n_c=∑_{i=1}^n𝛾_i^c.
>   $$
>   $$
>     𝜇_c^{(t+1)}⟵1/n_c∑_{i=1}^n𝛾_i^c x_i.
>   $$
>   $$
>     Σ_c^{(t+1)}⟵1/n_c∑_{i=1}^n𝛾_i^c (x_i−𝜇_c^{(t+1)})(x_i−𝜇_c^{(t+1)})^T.
>   $$
>   $$
>     𝜋_c^{(t+1)}⟵n_c/n.
>   $$
>   $$
>     t⟵t+1
>   $$
>
>    * **Return** $\hat{𝜋}, \hat{𝜇}, \hat{Σ}$. 

* Relation to k-Means: 
  * If we fix the cluster covariance matrix to be $𝜎^2I$, 
  * As we take $𝜎^2⟶0$, the update equations converge to doing k-means. 
  * Soft assignments converge to hard assignments (because of the tail behavior of Gaussian).
