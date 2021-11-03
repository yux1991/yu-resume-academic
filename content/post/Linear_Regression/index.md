---
title: Linear Regression
subtitle: A review of the linear regression.

# Summary for listings and search engines
summary: This article summarizes the key points of linear regression including assumption, formulization and the model performance.

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

#### What is the assumption of linear regression?

* Assumption: as we change $X$, the only thing that can possibly change about the conditional distribution of $Y$ given $(X_1, . . . , X_k)$, is the conditional mean $E(Y∣X_1, . . . , X_k)$. 

* General form of the regression model: General form of the regression model:
$$
  Y=E(Y∣X_1,⋯,X_k)+Z.
$$ 

* Least-square principle: Suppose we have a random variable $Y$, and we want to estimate $E(Y)$ based on a sample $(y_1, . . . , y_n)$. The least-squares principle says that we select the point $t(y_1, . . . , y_n)$, in the set of possible values for $E(Y)$, that minimizes the sum of squared  deviations (hence, “least squares”) given by 
$$
  ∑_{i=1}^n(y_i−t(y_1,⋯,y_n))^2. 
$$
Such an estimate is called the **least-squares estimate**. 
