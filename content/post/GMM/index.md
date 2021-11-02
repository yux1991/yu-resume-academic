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

## Overview

1. Gaussian Mixture Model Parameters (k Components): 
  * Clustering probabilities: 
    
    $$ 𝜋=(𝜋_1,⋯𝜋_k) $$
    
  * Cluster means: 
    * 𝜇=(𝜇1,⋯,𝜇k)
  * Cluster covariance matrices: 
    * Σ=(Σ1,⋯,Σk)
 
2. Joint Distribution: 

  * p(x,z)=p(z)p(x∣∣z)=𝜋z𝒩(x∣∣𝜇z,Σz).
 
  * Notes: 
    * x|z has distribution 𝒩(𝜇z,Σz). z corresponds to (x is the true cluster assignment). 
    * Suppose we know the model parameters 𝜋z,𝜇z,Σz, then it is easy to evaluate the join density p(x,z). 

Latent Variable Model: 

[Definition] A latent variable model is a probability model for which certain variables are never observed. 

Example: 

In the Gaussian mixture model, we don't observe 
z
 (the cluster assignment). Therefore 
z
 is a latent variable, or a hidden variable. 

The GMM "Inference" Problem: 

Suppose we observe 
x
, we want to know its cluster assignment 
z
. 

The conditional probability for cluster 
z
 given 
x
 is: 

p(z∣∣x)=p(x,y)p(x).
 

The conditional distribution is a soft assignment to clusters. 

A hard assignment is: 

z∗=argmaxz∈{1,⋯,k}p(z∣∣x).
 

If we have the model, the inference is trivial. 

Mixture Models: 

Margin Distribution: 

[Definition] The margin distribution for a single observation 
x
 is: 

p(x)=∑kz=1p(x,z)=∑kz=1𝜋z𝒩(x∣∣𝜇z,Σz).
 

Notes: 

p(x)
 is a convex combination of probability densities. 

Mixture Distributions (or Mixture Models): 

[Definition] A probability density 
p(x)
 represents a mixture distribution or mixture model, if we can write it as a convex combination of probability densities. That is: 

p(x)=Σki=1wipi(x),
 

where 
wi≥0
, 
Σki=1wi=1
, and each 
pi
 is a probability density. 

Notes: 

In the GMM, 
x
 has a mixture distribution. 

More constructively, let 
S
 be a set of probability distributions: 

Choose a distribution randomly from 
S
. 

Sample 
x
 from the chosen distribution. 

Then 
x
 has a mixture distribution. 

The GMM "Learning" Problem: 

Statement of the problem: 

Given data 
x1,⋯,xn
 drawn from a GMM. 

Estimate the parameters 
𝜋z,𝜇z,Σz
. 

Review: Estimating a Gaussian Distribution: 

The density for 
x∼𝒩(𝜇,Σ)
 is: 

p(x∣∣𝜇,Σ)=1|2𝜋Σ|‾‾‾‾‾√exp(−12(x−𝜇)TΣ−1(x−𝜇)).
 

The log-density is: 

logp(x∣∣𝜇,Σ)=−12log|2𝜋Σ|−12(x−𝜇)TΣ−1(x−𝜇).
 

The log joint density from a sample 
x1,⋯,xn
 i.i.d. from a 
𝒩(𝜇,Σ)
 distribution is: 

J(𝜇,Σ)=∑ni=1logp(x∣∣𝜇,Σ)=−n2log|2𝜋Σ|−12∑ni=1(x−𝜇)T𝛴−1(x−𝜇).
 

To estimate 
𝜇
 and 
Σ
 from a sample 
x1,⋯,xn
 i.i.d. from a 
𝒩(𝜇,Σ)
 distribution, we need to maximize the log joint density: 

∇𝜇J(𝜇,Σ)=0⟹𝜇ˆMLE=1n∑ni=1xi.
 

∇ΣJ(𝜇,Σ)=0⟹ΣˆMLE=1n∑ni=1(xi−𝜇ˆMLE)T(xi−𝜇ˆMLE).
 

Estimating the GMM using maximum likelihood: 

Find parameter values with highest likelihood for the observed data. 

The model likelihood for 
𝒟=(x1,⋯,xn)
 sampled i.i.d. from a GMM is: 

L(𝜋,𝜇,Σ)=∏ni=1p(xi)
 

        =∏ni=1∏kz=1𝜋z𝒩(xi∣∣𝜇z,Σz).
 

The objective function is: 

J(𝜋,𝜇,Σ)=∑ni=1log{∑kz=1𝜋z𝒩(xi∣∣𝜇z,Σz)}.
 

Plugging in the probability density for 
𝒩(𝜇,Σ)
, we get the GMM log-likelihood: 

J(𝜋,𝜇,Σ)=∑ni=1log{∑kz=1𝜋z∣∣2𝜋Σz∣∣‾‾‾‾‾‾√exp(−12(x−𝜇z)TΣ−1(x−𝜇z))}.
 

Issues with MLE for GMM: 

No closed form expression for MLE. 

There are 
k!
 equivalent solutions. 

The likelihood goes to infinity as 
𝜎2⟶0
 for some outliers. 

Keep restarting optimization. 

Bayesian approach. 

Running SGD on the GMM log-likelihood objective can be done in principle, but is challenging. 

The EM Algorithm for GMM: 

Estimating a Fully-Observed GMM: 

Suppose we observe 
(x1,z1),⋯,(xn,zn)
 i.i.d. from GMM 
p(x,z)
. Then find MLE is easy: 

nz=∑ni=1𝟏(zi=z).
 

𝜋ˆ(z)=nzn.
 

𝜇ˆz=1nz∑i:zi=zxi.
 

Σˆz=1nz∑i:zi=z(xi−𝜇ˆz)(xi−𝜇ˆz)T.
 

Cluster Responsibilities: 

Denote the probability that observed value 
xi
 comes from cluster 
j
 by: 

𝛾ji=p(z=j∣∣x=xi),
 

which is the responsibility that cluster 
j
 takes for observation 
xi
. 

Given the parameters 
𝜋z,𝜇z,Σz
, it is easy to find: 

𝛾ji=p(z=j∣∣xi)
 

      =p(z=j,xi)p(xi)
 

      =𝜋j𝒩(xi∣∣𝜇j,Σj)∑kc=1𝜋c𝒩(xi∣∣𝜇c,Σc).
 

The vector 
(𝛾1i,⋯,𝛾ki)
 is exactly the soft assignment for 
xi
. 

Algorithm: 

Algorithm: EM algorithm for GMM 

Input: 
𝒟={x1,⋯,xn}⊂𝒳
. 

GMM (
k
 components): 
𝜋=(𝜋1,⋯𝜋k)
, 
𝜇=(𝜇1,⋯,𝜇k)
, 
Σ=(Σ1,⋯,Σk).
 

Initialize: 
𝜋(0),𝜇(0),Σ(0),t=0.
 

While not converge: 

For 
i=1,⋯,n
 and 
j=1,⋯,k
: 

𝛾ji=𝜋(t)j𝒩(xi∣∣𝜇(t)j,Σ(t)j)∑kc=1𝜋c𝒩(xi∣∣𝜇c,Σc)
 // the "E step 

For 
c=1,⋯,k
: // the "M step 

nc=∑ni=1𝛾ci.
 

𝜇(t+1)c⟵1nc∑ni=1𝛾cixi.
 

Σ(t+1)c⟵1nc∑ni=1𝛾ci(xi−𝜇(t+1)c)(xi−𝜇(t+1)c)T.
 

𝜋(t+1)c⟵ncn.
 

t⟵t+1
 

Return 
𝜋ˆ, 𝜇ˆ, Σˆ
. 

Relation to 
k
-Means: 

If we fix the cluster covariance matrix to be 
𝜎2I
, 

As we take 
𝜎2⟶0
, the update equations converge to doing 
k
-means. 

Soft assignments converg
