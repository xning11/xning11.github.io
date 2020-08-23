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

$$
\newcommand{ind}[2]{ #1 \perp\!\!\!\perp #2}
\newcommand{cind}[3]{ #1 \perp\!\!\!\perp #2 \, | \, #3}
$$

This is a series of lecture note posts of [**Causal Inference: What If**](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/), by Miguel A. Hernán and James M. Robins (2020). The book provides a comprehensive plan for learning causal inference, both qualitatively and quantitatively, from definitions to methodologies to implications. It is an excellent book that worths the devotion of time to fully digest. So, I made these notes to summarize what I have learned and what I can use for my causal inference analysis.

To better use the notes, I would suggest that you read the book first. They shared many stories to make the technical points more interesting and relating. Then you can use the summary notes here to enhance your understanding of the topic. I hope you find them helpful.

The first note talks about the assumptions for causal inference, the definition of causal effect, the difference between causal inference and associative inference, randomized experiments, observational studies, and three identification conditions for making causal inference in observational data. (It covers the chapters 1-3 in the book.)

## A Definition of Causal Effect

Before we start, let's explicate the implicit assumptions when making causal inference. Vilation of these assumptions may induce improper causal inference of any intervention of interest.

1. *No Interference:* An individual's outcome is not influenced by their social interaction with other population members.
    - It means that individuals' outcomes ought to be independent of each other in the presence of intervention of interest.
    - In social networking experiments/obsevational studies, this assumption is unlikely to hold.
2. *Treatment Variation Irrelevance:* Multiple versions of treatment may exist but they all result in the same counterfactual outcome.
    - It means that the intervention should be well-defined and -measured.
    - In biostatistics, it is important to define specific variants of treatment and their corresponding outcomes.

Consider a dichotomous treatment variable $A$ (1: treated, 0: untreated) and a dichotomous outcome variable $Y$ (1: death, 0: survival), each takes on one of only two possible values when observed or measured. Let $Y^{a}$ be the outcome variable that would have been observed under the treatment value $A=a$. The variables $Y^{a=1}$ and $Y^{a=0}$ are referred to as counterfactual outcomes.

**Note:** For a binary $A$ and $Y$, $E[Y^{a}] = P[Y^{a}]$.
{: .notice--info}

An average causal effect of treatment $A$ on outcome $Y$ is present if $E[Y^{a=1}=1]\neq E[Y^{a=0}=1]$ in the population of interest. The corresponding null hypothesis of no average causal effect is defined as $E[Y^{a=1}]=E[Y^{a=0}]$, or equivalently, $E[Y^{a=1}-Y^{a=0}]=0$. Thus, rejection of the null indicates the presence of the average causal effect.

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

When measuring the causal effect, the problem is that we only observe one of the outcomes if the individual is treated or untreated. For example, the counterfactual outcomes under no treatment, $P(Y^{a=0}=1)$, cannot be directly computed. Besides, the counterfactual outcomes are likely nondeterministic, and vary across individuals.

**Note:** If $A=1$, the $Y^{a=0}$ is missing data. If $A=0$, the $Y^{a=1}$ is missing data.
{: .notice--info}

Now let's turn to the definition of association. Similarly, there are three types of measures of association under the null:

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

When the proportion of individuals who develop the outcome in the treated $P(Y=1 \vert A=1)$ equals the proportion of individuals who develop the outcome in the untreated $P(Y=1 \vert A=0)$, we say that treatment $A$ and outcome $Y$ are independent, that $A$ is not associated with $Y$, $\ind{Y}{A}$. However, treatment $A$ and outcome $Y$ are dependent or associated when $P(Y=1 \vert A=1) \neq P(Y=1 \vert A=0)$.

#### Difference between Causation and Association

Notably, the risk $P(Y=1 \vert A=a)$ is a conditional probability: the risk of $Y$ in the subset of the population that have actually received treatment value $a$, $A=a$. They can be measured directly. In contrast, the risk $P(Y^{a})$ is an unconditional/marginal probability: the risk of $Y^{a}$ in the whole population. They can not be measured because of missing data.

![image-center]({{ site.url }}{{ site.baseurl }}/images/causalinf-fig1-1.png){: .align-center}

In essence, **association is not causation**. Causation is defined by a different risk in the same population under the two different treatment values, $P(Y^{a}=1)$, $a=1$ or $a=0$. That is, causal inference is concerned with *what if*, what would be the risk if everybody had been treated or untreated?

Association is defined by a different risk in two disjoint subsets of the population determined by the individual's actual treatment value, $P(Y=1 \vert A=a)$, $A=1$ or $A=0$. Thus, associative inference is concerned with *reality*, what is the risk in the treated or the untreated?

In real word data, we can only observe the outcomes that indeed happened. The question is then under which conditions real world data can be used for causal inference. One approach is to conduct randomized experiments.

## Randomized Experiments

Randomized experiments generate data with missing values of the counterfactual outcomes. However, randomization ensures that those missing values occurred by chance. 

To make causal inference in randomized experiments, *exchangeability* is required. When the group membership is randomized, which particular group received the treatment is irrelevant for the value of $P(Y=1 \vert A=1)$ and $P(Y=1 \vert A=0)$.

$$ P(Y^{a}=1 \vert A=1) = P(Y^{a}=1 \vert A=0) = P(Y^{a}=1) $$

It means that the counterfactual risk under treatment value $a$ is the same in both groups $A=1$ and $A=0$. The treated and the untreated would have experienced the same risk of death if they had received the same treatment level (either $a=0$ or $a=1$). Thus, in ideal randomized experiments, association *is* causation.

$$
\begin{aligned}
P(Y^{a=1}=1) &= P(Y=1 \vert A=1) \\
P(Y^{a=0}=1) &= P(Y=1 \vert A=0)
\end{aligned}
$$

Formally, exchangeability is defined as independence between the counterfactual outcome and the actual treatment.

$$ \ind{Y^{a}}{A}, \forall a $$

When the treated and the untreated are exchangeable, we say that treatment is exogenous. Exogeneity is commonly used as a synonym for exchangeability. 

In practice, we are generally unable to determine whether exchangeability holds in our study. However, it is still possible that a study is a randomized experiment if exchangeability does not hold.

With some prognostic factor $L$ measured before treatment was assigned, we can conduct a study that is a randomized experiment with randomization conditional on $L$. We call it a *conditionally randomized experiment*.

Conditional randomization ensures that the treated and the untreated are exchangeable in the subset of individuals in the population, e.g., $L=1$ and $L=0$.

$$
\begin{aligned}
P(Y^{a}=1 \vert A=1, L=1) &= P(Y^{a}=1 \vert A=0, L=1)  \\
P(Y^{a}=1 \vert A=1, L=0) &= P(Y^{a}=1 \vert A=0, L=0)
\end{aligned}
$$

Formally, conditional exchangeability is defined as independence between $Y^{a}$ and $A$ in different subsets of the population where $L=l$ for all $l$.

$$ \cind{Y^{a}}{A}{L}, \forall a $$

In conditionally randomized experiments, we can compute the average causal effect in each of these subsets or strata of the population. Because association is causation within each subset, the stratum-specific causal risk ratio $\frac{P(Y^{a=1}=1 \vert L=1)}{P(Y^{a=0}=1 \vert L=1)}$ among people within $L=1$ is equal to the stratum-specific associational risk ratio $\frac{P(Y=1 \vert L=1, A=1)}{P(Y=1 \vert L=1, A=0)}$ among people within $L=1$. And analogously for $L=0$.

This method to compute stratum-specific causal effects is referred to as stratification. If the stratum-specific causal effects in each subset are different, we say that the treatment effect is modified by $L$, or that there is effect modification by $L$.

#### Standardization and Inverse Probability Weighting

There are two methods to compute the average causal effects in the whole population in a conditionally randomized experiment: standardization and inverse probability weighting.

TBC

$$ \ind{Y_{i}}{X} $$

$$ \cind{Y_{i}}{X}{Z} $$