---
title: "Bias-Variance-Noise Decomposition"
categories:
  - machine learning
tags:
  - bias-variance
---

This post is about bias-variance-noise decomposition in modeling.

Suppose that we have a training set $$D=\{(x_{1},y_{1}),...(x_{n},y_{n})\}$$ that can be expressed with a linear function $$y=f(x)+\varepsilon$$, where the noise $$\varepsilon$$ has mean zero and variance $$\sigma^{2}$$. 

To understand the relationship, we hypothesize a function $$\hat{f}(x;D)$$ that approximates the true function $$f(x)$$ by measuring the mean squared error between $$y$$ and $$\hat{f}(x;D)$$ - here I use MSE loss function of regression problem as an example. Ideally, we want our $$MSE = \frac{1}{n}\sum(y-\hat{f}(x;D))^{2}$$ to be minimal for both the training data and test points. 

For a selected function $$\hat{f}(x;D)$$, we can decompose its expected generalization error on the test set as,

$$
E_{D}[(y-\hat{f}(x;D))^{2}] = (Bias_{D}[\hat{f}(x;D)])^{2} + Var_{D}[\hat{f}(x;D)] + \sigma^{2}
$$

where 

$$
\begin{aligned}
Bias_{D}[\hat{f}(x;D)] &= E_{D}[\hat{f}(x;D)] - f(x) \\ 
Var_{D}[\hat{f}(x;D)] &= E_{D}[\hat{f}(x;D)^{2}] - E_{D}[\hat{f}(x;D)]^{2}.\end{aligned}
$$

To derive the above decomposition, recall that $$y=f(x)+\varepsilon$$, the true function $$f$$ is deterministic, i.e. independent of $$D$$; the noise $$\varepsilon$$ is irreducible error that represents the difference between the true function and the observed data. Given that 

$$
\begin{aligned}
E(y) &= E[f(x)]+E[\varepsilon] = E[f(x)] = \bar{y} \\ 
V(y) &= E[(y-E[y])^{2}] = E[\varepsilon^{2}] = \sigma^{2} 
\end{aligned}
$$

we can show that, 

$$
\begin{aligned}
E_{D}[(y-\hat{f})^{2}] 
    &= E_{D}[(f + \varepsilon - \hat{f}]^{2} \\ 
    &= E_{D}[(f + \varepsilon - \hat{f} + E[\hat{f}] - E[\hat{f}]]^{2} \\ 
    &= E_{D}[(f - E[\hat{f}] + E[\hat{f}] - \hat{f} + \varepsilon]^{2} \\ 
    &= [f - E[\hat{f}]]^{2} + E[(\hat{f} - E[\hat{f}])^{2}] + E[\varepsilon^{2}] \\ 
    &= Bias[\hat{f}]^{2} + Var[\hat{f}] + \sigma^{2}.  
\end{aligned}
$$

Essentially, the bias term is the difference between the expected outcomes of the selected model and the true outcomes, the variance term is the variability of the selected model due to the sampling of data, and the noise term is the random error in the problem itself.

----
References:

1. [Wikipedia: Bias–variance tradeoff](https://en.wikipedia.org/wiki/Bias%E2%80%93variance_tradeoff)
2. [https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote12.html](https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote12.html)
