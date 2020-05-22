---
title: "Naive Bayes Classifier"
categories:
  - machine learning
tags:
  - naive bayes
  - classifier
---

This post is about Naive Bayes Classifier and the link between Naive Bayes classifier and Logistic Regression.

From the Bayesian perspective, for a training dataset $$D = \{(x^{(1)},y^{(1)}),...,(x^{(n)},y^{(n)})\}$$, we model the posterior distribution over the parameters $$\theta$$,

$$
P(\theta \vert D) = \frac{P(D \vert \theta)P(\theta)}{P(D)}
$$

using the likelihood of the data given the parameters, $$P(D \vert \theta)$$, and the prior distribution over the parameters, $$P(\theta)$$.

We use the Maximum A Posterior (MAP) estimates to solve for the parameters, $$\hat \theta_{MAP} = argmax_{\theta} P(\theta \vert D) \propto P(D \vert \theta)P(\theta)$$. To make predictions about the label $$y$$ of a test sample with features $$x$$, we use

$$
P(y \vert x,D) = \int_{\theta} P(y,\theta \vert x,D) d\theta = \int_{\theta} P(y \vert x,\theta,D) P(\theta \vert D) d\theta.
$$

For Naive Bayes, we assume that feature values are independent given the label, $$P(x \vert y) = \prod_{j}^{d} P(x_{j} \vert y)$$. In this case, the Naive Bayes classifier can be defined as,

$$
\begin{aligned}
h_{\theta}(x) &= argmax_{y} P(y \vert x) \\
     &= argmax_{y} \frac{P(x \vert y)P(y)}{P(x)} \\
     &= argmax_{y} P(x \vert y)P(y) \\
     &= argmax_{y} \prod_{j}^{d} P(x_{j} \vert y) P(y) \\
     &= argmax_{y} \sum_{j}^{d} \log(P(x_{j} \vert y)) + \log(P(y))
\end{aligned}
$$

One can show that Naive Bayes classifier is a linear classifier. In the case of continuous features, (Gaussian) Naive Bayes classifier is approximate to logistic regression (with the logistic loss function), provided the conditional independence assumption holds. The posterior distribution can be derived as,

$$
\begin{aligned}
P(y \vert x,\theta) = \frac{1}{1+e^{-y(\theta'x)}}.
\end{aligned}
$$

Formally, we derive the MAP estimate function as, 

$$
\begin{aligned}
\hat{\theta}_{MAP} &= argmax_{\theta} \prod_{i}^{n}P(y^{(i)} \vert x^{(i)},\theta)P(\theta) \\
                   &= argmin_{\theta} \sum_{i}^{n} \log(1+e^{-y^{(i)}\theta'x^{(i)}}) + \lambda \theta'\theta.
\end{aligned}
$$

One caveat about Naive Bayes Classifier is the presence of zero in probability. It can't work in cases where an event (a set of feature values) hasn't been observed, i.e., $$P(x \vert y)=0$$. To avoid zeros in the probability estimation, we can use MAP estimation with Beta priors, or apply Laplace smoothing.

The Bayesian approach is one example of generative learning (by estimating $$P(x,y)=P(x \vert y)P(y)$$), which is different from logistic regression as one example of discriminative learning (by estimating $$P(y \vert x)$$).

In logistic regression, we model the parameters that maximize the likelihood of the data, $$P(y \vert x;\theta)$$, assuming the data are drawn from a certain distribution $$D \sim \mathbb{P}$$. We use the maximum likelihood estimates (MLE) to solve for the parameters, $$\hat \theta_{MLE} = argmax_{\theta} P(y \vert x;\theta)$$. Formally,

$$
\begin{aligned}
\hat{\theta}_{MLE} &= argmax_{\theta} \prod_{i}^{n}P(y^{(i)} \vert x^{(i)};\theta) \\
                   &= argmin_{\theta} \sum_{i}^{n} \log(1+e^{-y^{(i)}\theta'x^{(i)}}).
\end{aligned}
$$

Logistic regression can more easily overfit the training data than Naive Bayes classifier. To see this, the optimization of Naive Bayes classifier takes into account both the likelihood of the data given the parameters and the prior of the parameters. The prior term is indeed a form of regularization that logistic regression doesn't have. Also, Naive Bayes classifier simply assumes conditional independence of feature values, thus the parameters are learned independently. Logistic regression allows the possible correlation of features, thus the parameters are learned collaboratively.

To solve Naive Bayes classifier and logistic regression, we use Gradient Descent or Newton's Method.

____
References:

1. [http://cs229.stanford.edu/notes2020spring/cs229-notes2.pdf](http://cs229.stanford.edu/notes2020spring/cs229-notes2.pdf)
2. [https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote05.html](https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote05.html)
3. [https://alliance.seas.upenn.edu/~cis520/dynamic/2019/wiki/index.php?n=Lectures.NaiveBayes](https://alliance.seas.upenn.edu/~cis520/dynamic/2019/wiki/index.php?n=Lectures.NaiveBayes)
4. [https://www.cs.cmu.edu/~tom/mlbook/NBayesLogReg.pdf](https://www.cs.cmu.edu/~tom/mlbook/NBayesLogReg.pdf)
