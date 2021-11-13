---
title: Deep Feedforward Networks
subtitle: Learning materials for the deep feedforward networks.

# Summary for listings and search engines
summary: This article summarizes the key points of deep feedforward networks.

# Link this post with a project
projects: []

# Date published
date: "2021-11-05T00:00:00Z"

# Date updated
lastmod: "2021-11-05T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
image:
  caption: 'Image credit: [**Springer**](https://link.springer.com/chapter/10.1007%2F978-3-319-69775-8_2)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Deep Learning


categories:
- Learning

---
### Introduction

#### What is the deep feedforward networks?

**Deep feedforward networks**, also called **feedforward neural networks**, or **multilayer perceptrons** (MLPs), are the quintessential deep learning models.The goal of a feedforward network is to approximate some function $f*$. These models are called *feedforward* because there are no *feedback* connections.

#### What are the components of a deep feedforward network?

A general form of a deep feedforward network can be represented by:

$$
  f(\textbf{x}) = f^{(n)}(f^{(n-1)}(\cdots(f^{(2)}(f^{(1)}(\textbf{x})))))
$$

* n-th Layer: $f^{(n)}$
* Output Layer: the final layer of a feedforward network
* Hidden Layers: The training examples specify directly what the output layer must do at each point $x$; it must produce a value that is close to $y$. The behavior of the other layers is not directly speciﬁed by the training data. Therefore the other layers are called **hidden layers**.
* Width: the dimensionality of the hidden layers.

#### How to understand the deep feedforward networks?

It is best to think of feedforward networks as **function approximation machines** that are designed to achieve statistical generalization, occasionally drawing some insights from what we know about the brain, rather than as models of brain function.

#### Nonlinear mapping 

Feedforward networks can also be thought of as an extention to the linear models by applying a nonlinear mapping $\phi$ to the input $\textbf{x}$. Instead of using a very generic $\phi$ (e.g. RBF kernel) or manual engineering, the strategy of deep learning is to learn $\phi$:
$$
  y=f(\textbf{x}; \theta,\textbf{w}) = \phi(\textbf{x}; \theta)^T\textbf{w}
$$
where we parameterize the representation as $\phi(\textbf{x}; \theta)$ and use the optimization algorithm to find the $\theta$ that corresponds to a good representation.

### An Example: Learning XOR

#### Statement of the problem

The XOR function (“exclusive or”) is an operation on two binary values, $x_1$ and $x_2$. When exactly one of these binary values is equal to 1, the XOR function returns 1. Otherwise, it returns 0. The XOR function provides the target function $y=f^*(x)$ that we want to learn. Our model provides a function $y=f(x;θ)$, and our learning algorithm will adapt the parameters $\theta$ to makef as similar as possible to $f^∗$.

#### Loss function
$$
  J(\mathbf{\theta}) = \frac{1}{4}\sum_{x\in\mathbb{X}}(f^*\mathbf(x) - f(\mathbf(x);\mathbf{\theta})^2)
$$

In practice, MSE is usually not an appropriate cost function for modeling binary data.

#### How the feedforward network work?

The network contains two functions chained together:
$$
  \mathbf{h}=f^{(1)}(\mathbf{x;W,c})
$$
and
$$
  y=f^{(2)}(\mathbf{h;w},b)
$$
with the complete model being:
$$
f(\mathbf{x;W,c;w},b)=f^{(2)}(f^{(1)}(\mathbf{x}))
$$

#### How to choose $f^{(1)}$?
$f^{(1)}$ cannot be a linear function, otherwise it becomes a linear model. Most neuralnetworks uses an aﬃne transformation controlled by learned parameters,followed by a ﬁxed nonlinear function called an activation function $g$:
$$
  \mathbf{h}=g(\mathbf{W}^T\mathbf{x}+\mathbf{c})
$$
where $W$ provides the weights of a linear transformation and $c$ the biases.

In modern neural networks,the default recommendation is to use the rectiﬁed linear unit, or ReLU [^1], deﬁned by the activation function
$$
  g(z) = \operatorname{max}(0, z)
$$

### Gradient-Based Learning

#### Cost Functions

* In most cases, our parametric model deﬁnes a distribution $p(\mathbf{y | x};\mathbf{\theta})$ and we simply use the principle of maximum likelihood. This means we use the **cross-entropy** between the training data and the model’s predictions as the costfunction.

  * The cross-entropy loss is:
    $$
    J(\mathbf{\theta})=-\mathbb{E}\_{\mathbf{x,y}\sim\hat{p}\_{data}}\log{p\_{model}(\mathbf{y}\vert\mathbf{x})}
    $$

  * The specific form depends on the distribution.
  * If $p_{model}(\mathbf{y}|\mathbf{x})=\mathcal{N}(\mathbf{y};f(\mathbf{x;\theta}),I)$, then we can recover the MSE cost:
    $$
    J(\mathbf{\theta})=\frac{1}{2}\mathbb{E}_{\mathbf(x,y)\sim\hat{p}_{data}} \parallel\mathbf{y}-f(\mathbf{x;\theta})\parallel^2+cost
    $$
  * Advantage: specifying a model $p(\mathbf{y | x};\mathbf{\theta})$ automatically determines a cost function $\log p_{model}(\mathbf{y}|\mathbf{x})$.
  * Disadvantage: usually no minimum value.

* Sometimes rather than predicting a complete probability distribution over $\mathbf{y}$, we merely predict some statistic of $\mathbf{y}$ conditioned on $\mathbf{x}$. Specialized loss functions enable us to train a predictor of these estimates. 
  * Solving the optimization problem with the **mean squared error** (MSE):
  $$
  f^{\*}=\underset{f}{\operatorname{argmin}}\ \mathbb{E}\_{\mathbf{x,y}\sim p\_{data}}\parallel\mathbf{y}-f(\mathbf{x})\parallel^2
  $$

  yields
  $$
  f^{\*}(\mathbf{x})=\mathbb{E}\_{\mathbf{x,y}\sim p\_{data}(\mathbf{y}\vert\mathbf{x})}[\mathbf{y}]
  $$

  * Solving the optimization problem:
  $$
  f^{\*}=\underset{f}{\operatorname{argmin}}\ \mathbb{E}\_{\mathbf{x,y}\sim p\_{data}}\parallel\mathbf{y}-f(\mathbf{x})\parallel\_1
  $$

  yields a function that predicts the *median* value of $\mathbf{y}$ for each $\mathbf{x}$. This cost function is commonly called **mean absolute error** (MAE).

* The total cost function used to train a neural network will often combine one of the primary cost functions with a regularization term.

#### Output Units

* Suppose that the feedforward network provides a set of hidden features deﬁned by $h=f(x;θ)$.
* The role of the output layer: provide some additional transformation from the features to complete the task.
* Linear Units
  * Formula:
  $$
    \mathbf{\hat{y}}=\mathbf{W^Th}+\mathbf{b}
  $$
  * Linear output layers are often used to produce the mean of a conditional Gaussian distribution:
  $$
    p(\mathbf{y}|\mathbf{x})=\mathcal{N}(\mathbf{y;\hat{y},I})
  $$
  Maximizing this log-likelihood $\log{p(\mathbf{y}|\mathbf{x})}$ is then equivalent to minimizing the MSE. 
  * For the linear unit, the covariance of the Gaussian is straightforward to learn, but the covariance must be constrained to be a positive definite matrix for all input.

* Sigmoid Units
  * Formula:
  $$
    \hat{y}=\sigma(w^T\mathbf{h}+b)
  $$

    where $\sigma$ is the logistic sigmoid function:

  $$
    \sigma(x)=\frac{1}{1+\exp{(-x)}}
  $$

{{< figure src="sigmoid.png" caption="Figure 1. The Sigmoid function" theme="light" >}}

  * Benefit of the Sigmoid function:
    * There is always a strong gradient whenever the model has the wrong answer.
  * Two components:
    * The **logit**:
    $$
      z=w^T\mathbf{h}+b
    $$
    * sigmoid activation function to conver $z$ into a probability.
  * Assume that the unnormalized log probabilies $\tilde{P}(y)$ are linear in $y$ and $z$, then:
    $$
      \log{\tilde{P}(y)}=yz
    $$

    $$
      \tilde{P}(y)=\exp{yz}
    $$

    $$
      P(y)=\frac{\exp{(yz)}}{\sum_{y'=0}^1 \exp{(y'z)}}
    $$

    $$
      P(y)=\sigma((2y-1)z)
    $$
  * The loss function for maximum likelihood learning of a Bernoulli parametrized by a sigmoid is:
    $$
      J(\mathbf{\theta})=-\log{P(y|x)}
    $$

    $$
      =-\log{\sigma((2y-1)z)}
    $$

    $$
      =\zeta((1-2y)z)
    $$

    where $\zeta$ is the **softplus** function.
  
  {{< figure src="softplus.png" caption="Figure 2. The Softplus function" theme="light" >}}

  * Maximum likelihood is almost always the preferred approach to training sigmoid output units because when $z$ has the wrong sign, derivative of softplus function with respect to $z$ asymptotes to $sign(z)$. This is useful because the gradient-based learning can act to quickly correct a mistaken $z$.


[^1]: [Nair V, Hinton GE. Rectified linear units improve restricted boltzmann machines. InIcml 2010 Jan 1.](https://icml.cc/Conferences/2010/papers/432.pdf)