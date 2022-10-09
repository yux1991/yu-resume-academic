---
title: Linear Regression
subtitle: A review of the linear regression.

# Summary for listings and search engines
summary: This article summarizes the key points of linear regression including assumption, formulization and the model performance.

# Link this post with a project
projects: []

# Date published
date: "2021-11-02T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Scikit-learn**](https://scikit-learn.org/stable/auto_examples/linear_model/plot_nnls.html#sphx-glr-auto-examples-linear-model-plot-nnls-py)'
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

#### Least-square principle

* Suppose we have a random variable $Y$, and we want to estimate $E(Y)$ based on a sample $(y_1, . . . , y_n)$. The least-squares principle says that we select the point $t(y_1, . . . , y_n)$, in the set of possible values for $E(Y)$, that minimizes the sum of squared  deviations (hence, “least squares”) given by 

$$
  ∑_{i=1}^n(y_i−t(y_1,⋯,y_n))^2. 
$$

Such an estimate is called the **least squares estimate**. 

### Simple Linear Regression

* Formula 

$$
  E((Y_1,\cdots,Y_n)|X_1=x_1, \cdots, X_n=x_n)
$$
$$
  =(\beta_1+\beta_2x_1, \cdots, \beta_1+\beta_2x_n )^T
$$

* LS estimates: 
  * $\beta_1=\bar{y}−\beta_2\bar{x}$.
  * $\beta_2=\frac{∑_{i=1}^n(x_i−\bar{x})(y_i−\bar{y})}{∑_{i=1}^n(x_i−\bar{x})^2}$.
 
* LS predictions: 
  * $E(B_1∣X_1=x_1,⋯,X_n=x_n)=\beta_1$.
  * $E(B_2∣X_1=x_1,⋯,X_n=x_n)=\beta_2$.
 
* LS standard errors: 
  * $Var(B_1∣X_1=x_1,⋯,X_n=x_n)=\sigma^2(\frac{1}{n}+\frac{\bar{x}^2}{∑_{i=1}^n(x_i−\bar{x})^2})$.
  * $Var(B_2∣X_1=x_1,⋯,X_n=x_n)=\frac{\sigma^2}{∑_{i=1}^n(x_i−\bar{x})^2}$.
  * $  E(S_2∣X_1=x_1,⋯,X_n=x_n)=\sigma^2$, while: 
$$
  s=\frac{1}{n−2}∑_{i=1}^n(y_i−b_1−b_2x_1)^2.
$$ 

* ANOVA (analysis of variance table) decomposition: 
$$
  ∑_{i=1}^n(y_i−\bar{y})^2=b_2^2∑_{i=1}^n(x_i−\bar{x})^2
$$
$$
  +∑_{i=1}^n(y_i−b_1−b_2x_i)^2.
$$
  * Regression sum of squares (RSS): measuring changes in the response due to changes in the predictor. 
$$
  RSS=b_2^2∑_{i=1}^n(x_i−\bar{x})^2.
$$ 

  * Error sum of squares (ESS): measuring changes in the response due to the contribution of random error. 
$$
  ESS=∑_{i=1}^n(y_i−b_1−b_2x_i)^2.
$$ 

* F-statistics: 
$$
  F=\frac{RSS}{ESS/(n−2)}
$$ 
$$
  =\frac{b_2^2∑_{i=1}^n(x_i−\bar{x})^2}{s^2}∼F(1,n−2).
$$

  * If $H_0: \beta_2=0$ is true, then $F=1$, which indicates no relationship between response and predictor. 
  * If $F≫1$, we should reject $H_0$. 

* ANOVA test or F-test: 
  * Null hypothesis $H_0:\beta_2=0$. 
  * P value: 
$$
  P(F≥\frac{b_2^2∑_{i=1}^n(x_i−\bar{x})^2}{s^2}).
$$ 

* The Coefficient of Determination: 
  * [Definition] The proportion of the observed variation in the response explained by changes in the predictor: 
$$
  R^2=\frac{b_2^2∑_{i=1}^n(x_i−\bar{x})^2}{∑_{i=1}^n(y_i−\bar{y})^2}.
$$ 

  * $R^2$ near 1: highly accurate predictions. 
  * $R^2$ near 0: not accurate. 

### General Linear Regression: 

* Matrix form: 
$$
  𝐲=𝐗\bf{\beta}+\bf{\epsilon}.
$$

Where: 

$$
  𝐲=(y_1, y_2, \cdots, y_n)_{n\times1}^T, 
$$

$$
  𝐗=(1, X_{1}, X_{2}, \cdots, X_{d})_{n\times d},
$$

$$
  \beta=(\beta_1, \beta_2, \cdots, \beta_d)_{d\times1}^T, 
$$

$$
  \epsilon=(\epsilon_1, \epsilon_2, \cdots, \epsilon_n)_{n\times1}^T.
$$ 

* The overdetermined system (n≥d) usually has no exact solution. Then OLS solution is found out by solving the quadratic minimizing problem: 
$$
  \hat{\bf{\beta}}=\underset{{\bf{\beta}∈ℝ^d}}{\operatorname{argmin}}\ S(\bf{\beta})
$$

Where: 
$$
  \hat{\bf{\epsilon}}=𝐲−\hat{\bf{\beta}}𝐗.
$$ 
$$
  S(\bf{\beta})=\hat{\bf{\epsilon}}^T\hat{\bf{\epsilon}}
$$
$$
  =∑_{i=1}^n∣y_i−∑_{j=1}^dx_{ij}\beta_j∣^2=‖𝐲−\bf{\beta}𝐗‖^2
$$
$$
=(𝐲−\bf{\beta}𝐗)^T(𝐲−𝐗\bf{\beta}).
$$ 

Provided that the d columns are linearly independent, the minimization has a unique solution: 
$$
  \hat{\bf{\beta}}=(𝐗^T𝐗)^{−1}𝐗^T𝐲.
$$ 

* OLS time complexity: 
$$
  O(n×d^2)
$$ 

* Some terminologies: 
  * Normal equation: 
$$
  (𝐗^T𝐗)\hat{\bf{\beta}}=𝐗^T𝐲.
$$ 

  * Normal matrix: 
$$
  𝐗^T𝐗.
$$ 

  * The predicted values: 
$$
  \hat{\bf{y}}=𝐗\hat{\bf{\beta}}=𝐗(𝐗^T𝐗)^{−1}𝐗^T𝐲=𝐏𝐲.
$$ 

  * The projection matrix: 
$$
  𝐏=𝐗(𝐗^T𝐗)^{−1}𝐗^T.
$$ 

  * The annihilator matrix: 
$$
  𝐌=𝐈_n−𝐏.
$$ 

  * The "centering" matrix: 
$$
  𝐂=𝐈_n−\frac{1}{n}𝐉_n,
$$
where $𝐉_n$ is an n-by-n matrix of all $1$'s. 

* Properties: 
  * Coefficient of determination: 
$$
  R^2=\frac{b_2^2∑_{i=1}^n(x_i−\bar{x})^2}{∑_{i=1}^n(y_i−\bar{y})^2}
$$ 
$$
=1−\frac{𝐲^T𝐌𝐲}{𝐲^T𝐂𝐲}=1−\frac{RSS}{TSS}.
$$

  * $𝐗^T\hat{\bf{\epsilon}}=0$.

  * Definitions:
$$
  RSS=∑_{i=1}^n(y_i−\hat{y})^2=𝐲^T𝐌𝐲=\hat{\bf{\epsilon}}^T\hat{\bf{\epsilon}}.
$$ 
$$
  ESS=∑_{i=1}^n(\hat{y}_i−\bar{y})^2=𝐲^T𝐏^T𝐋𝐏𝐲.
$$ 
$$
  TSS=∑_{i=1}^n(y_i−\bar{y})^2=𝐲^T𝐂𝐲.
$$ 
$$
  TSS=RSS+ESS.
$$ 