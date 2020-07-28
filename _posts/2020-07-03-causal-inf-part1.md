---
title: "Casual Inference - Causation vs Association, Randomized Experiments, and Observational Studies"
categories:
  - causal inf
tags:
  - causal effect
  - randomized-experiments
  - exchangeability
  - consistency
---

This is the first note of a series of lecture note posts of [**Causal Inference: What If**](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/), by Miguel A. Hernán and James M. Robins (2020). The book provides a comprehensive plan for learning causal inference, both qualitatively and quantitatively, from definitions to methodologies to implications. It is an excellent book that worths the devotion of time to fully digest. So, I made these notes to summarize what I have learned and what I can use for my causal inference analysis. I hope you will find them helpful as well.

The first note includes the assumptions for causal inference, the definition of causal effect, the difference between causal inference and associative inference, randomized experiments, observational studies, and three identification conditions for making causal inference in observational data. (It covers the chapters 1-3 in the book.)

## A Definition of Causal Effect

First, let's explicate the implicit assumptions when making causal inference. Vilation of these assumptions may induce improper causal inference of any intervention of interest.

1. *No Interference:* An individual's outcome is not influenced by their social interaction with other population members.
    - It means that individuals' outcomes ought to be independent of each other in the presence of intervention of interest.
    - In social networking experiments/obsevational studies, this assumption is unlikely to hold.
2. *Treatment Variation Irrelevance:* Multiple versions of treatment may exist but they all result in the same counterfactual outcome.
    - It means that the intervention should be well-defined and -measured.
    - In biostatistics, it is important to define specific variants of treatment and their corresponding outcomes.

For simplicity, consider a dichotomous treatment variable $A$ (1: treated, 0: untreated) and a dichotomous outcome variable $Y$ (1: death, 0: survival), each takes on one of only two possible values when observed or measured. Let $Y^{a}$ be the outcome variable that would have been observed under the treatment value $A=a$. The variables $Y^{a=1}$ and $Y^{a=0}$ are referred to as counterfactual outcomes.

By definition, an average causal effect of treatment $A$ on outcome $Y$ is present if $E[Y^{a=1}=1]\neq E[Y^{a=0}=1]$ in the population of interest. The corresponding null hypothesis of no average causal effect is $E[Y^{a=1}]=E[Y^{a=0}]$, or equivalently, $E[Y^{a=1}-Y^{a=0}=0]$. Thus, rejection of the null indicates the presence of the average causal effect.

There are three types of measures of causal effect under the null:

1. Causal risk differece - measuring the absolute number of cases of the outcome attributable to the treatment.
    $$
    P(Y^{a=1}=1) - P(Y^{a=0}=1) = 0
    $$

2. Causal risk ratio - measuring how many times treatment relative to no treatment increases the outcome of interest.
    $$
    \frac{P(Y^{a=1}=1)}{P(Y^{a=0}=1)} = 1
    $$

3. Causal odds ratio.
    $$
    \frac{P(Y^{a=1}=1)/P(Y^{a=1}=0)}{P(Y^{a=0}=1)/P(Y^{a=0}=0)} = 1
    $$

One of the difficulties in measuring the causal effect is that we only observe one of the outcomes if the individual is treated or untreated. For example, the counterfactual outcomes under no treatment, $P(Y^{a=0}=1)$, cannot be directly computed. Besides, the counterfactual outcomes are likely nondeterministic, and vary across individuals.

Instead, we define the measures of association under the null as follows:

1. Associative risk difference.
    $$
    P(Y=1 \vert A=1) - P(Y=1 \vert A=0) = 0
    $$

2. Associative risk ratio.
    $$
    \frac{P(Y=1 \vert A=1)}{P(Y=1 \vert A=0)} = 1
    $$

3. Associative odds ratio.
    $$
    \frac{P(YY=1 \vert A=1)/P(Y=0 \vert A=1)}{P(YY=1 \vert A=0)/P(Y=0 \vert A=0)} = 1
    $$

When the proportion of individuals who develop the outcome in the treated $P(Y=1 \vert A=1)$ equals the proportion of individuals who develop the outcome in the untreated $P(Y=1 \vert A=0)$, we say that treatment $A$ and outcome $Y$ are independent, that $A$ is not associated with $Y$, $Y \perp A$. However, treatment $A$ and outcome $Y$ are dependent or associated when $P(Y=1 \vert A=1) \neq P(Y=1 \vert A=0)$.

Looking carefully, the risk $P(Y=1 \vert A=a)$ is a conditional probability: the risk of $Y$ in the subset of the population that have actually received treatment value $a$, $A=a$. In contrast, the risk $P(Y^{a})$ is an unconditional/marginal probability: the risk of $Y^{a}$ in the whole population.

![image-center]({{ site.url }}{{ site.baseurl }}/images/causalinf-fig1-1.png){: .align-center}

To summarize, causation is defined by a different risk in the same population under the two different treatment values, $P(Y^{a}=1)$, $a=1$ or $a=0$. That is, causal inference is concerned with *what if*, what would be the risk if everybody had been treated or untreated? Association is defined by a different risk in two disjoint subsets of the population determined by the individual's actual treatment value, $P(Y=1 \vert A=a)$, $A=1$ or $A=0$. Thus, associative inference is concerned with *reality*, what is the risk in the treated or the untreated?

In essence, *association is not causation*. In real word data, we can only observe the outcomes that indeed happened. The question is then under which conditions real world data can be used for causal inference. One way is to conduct randomized experiments.

## Randomized Experiments

Randomized experiments generate data with missing values of the counterfactual outcomes. However, randomization ensures that those missing values occurred by chance.

To make causal inference in randomized experiments, *exchangeability* is required. When the group membership is randomized, which particular group received the treatment is irrelevant for the value of $P(Y=1 \vert A=1)$ and $P(Y=1 \vert A=0)$.

$$ P(Y^{a}=1 \vert A=1) = P(Y^{a}=1 \vert A=0) = P(Y^{a}=1) $$

It means that the counterfactual risk under treatment value $a$ is the same in both groups $A=1$ and $A=0$. The treated and the untreated would have experienced the same risk of death if they had received the same treatment level (either $a=0$ or $a=1$).

$$
\begin{aligned}
P(Y^{a=1}=1) &= P(Y=1 \vert A=1) \\
P(Y^{a=0}=1) &= P(Y=1 \vert A=0)
\end{aligned}
$$

Formally, exchangeability is defined as independence between the counterfactual outcome and the actual treatment.

$$ Y^{a} \perp A, \forall a $$

When the treated and the untreated are exchangeable, we say that treatment is exogenous. Exogeneity is commonly used as a synonym for exchangeability.

In practice, we are generally unable to determine whether exchangeability holds in our study. However, it is still possible that a study is a randomized experiment if exchangeability does not hold.

With some prognostic factor $L$ measured before treatment was assigned, we can conduct a study that is a randomized experiment with randomization conditional on $L$.

TBC
