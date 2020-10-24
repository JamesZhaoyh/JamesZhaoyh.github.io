---
layout: draftpost
title:  "Introduction to Monte Carlo Methods"
date:   2020-10-24 01:07:00 -0400
categories: MC notes
---
This note is part of my learning notes of Monte Carlo methods. It is also a test note. Further modifications will be made later.

## Some understanding about sampling

In MC, we want to use the expectation of a function $V$ a random variables (RV) $X$ to calculate the quantity of interest $A$:
$$
\tag{1}
A = \mathbb{E}[V(X)]
$$
where $X \sim \rho$.

In the real calculation, we do not evaluate the expectation directly. In stead, we use samples to estimate $A$:
$$
\tag{2}
\hat{A} = \sum_{k=1}^N V(X_k),
$$
where $X_k \sim \rho_k$. 

- In direct sampling, all $\rho_k$'s are the same, and $X_k$'s are i.i.d. RVs.
- In MCMC, $\rho_k$'s are generated from a MC. So $X_k$'s are dependent. 



### Statistical estimators

Before, we dive into two sampling methods, we first learn some basics about the statistical estimators. Usually, when we talk about a RV, the quantities are of the most importance of interest: the mean $\mu$ and the variance $\sigma^2$. The definitions are as follows. Let $X$ be a RV, then 
$$
\mu = \mathbb{E}[X], \\
\operatorname{Var}(X) = \sigma^2(X) = \mathbb{E}[(X-\mathbb{E}[X])^2] = \mathbb{E}[X^2]-\mathbb{E}[X]^2.
$$
The statistical estimators can estimate these theoretical values from a series of samples $X_1, \dots, X_n$. The estimators of $\mu$ and $\sigma^2$ are called **sample mean** and **sample variance**, which are defined as follows:
$$
\begin{align}
\bar{X} &= \frac{1}{n} \sum_{i=1}^{n} X_{i}, \tag{3} \label{3}\\
S^{2} &= \frac{1}{n} \sum_{i=1}^{n}\left(X_{i}-\bar{X}\right)^{2}. \tag{4}\label{4}
\end{align}
$$
There are some other interesting topics about the sample mean and the sample variance, for example, the bias of the estimators, see *Bias of an estimator wiki*. We will not discuss here. 

Note that $\bar{X}$ and $S^2$ are the standard estimator. **We just need to remember it**.

The covariance measures two RVs how $X$ and $Y$ are statistically related, which is defined as follows:
$$
\operatorname{Cov}(X,Y) = \mathbb{E}[(X-\mathbb{E}[x])(Y-\mathbb{E}[Y])] = \mathbb{E}[XY] - \mathbb{E}[X] \mathbb{E}[Y].
$$
For a sequence of RVs $X_1, \dots, X_n$, we have 
$$
\operatorname{var}(\sum_{k=1}^N X_k) = \sum_{i,j=1}^N\operatorname{Cov}(X_i, X_j) = \sum_{k=1}^N \operatorname{var}(X_k) + 2\sum_{i=1}^N\sum_{j=i+1}^N \operatorname{Cov}(X_i, X_j).
$$
Other properties of the covariance can be found in wiki. 

If $X$ and $Y$ are uncorrelated, they are **NOT** necessarily independent, but we can say
$$
\operatorname{Cov}(X, Y) = 0.
$$




### Direct sampling 

