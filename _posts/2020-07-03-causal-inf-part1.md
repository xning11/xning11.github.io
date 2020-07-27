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

This is a series of lecture note posts of [**Causal Inference: What If**](https://www.hsph.harvard.edu/miguel-hernan/causal-inference-book/), by Miguel A. Hernán and James M. Robins (2020). The book provides a comprehensive plan for learning causal inference, both qualitatively and quantitatively, from definitions to methodologies to implications. It is an excellent book that worths the devotion of time to fully digest. In the following note posts, I hope that you will find them helpful.

The first note includes the assumptions for causal inference, the definition of causal effects, the difference between causal inference and associative inference, randomized experiments, observational studies, and three identification conditions for making causal inference in observational data. (It covers the chapters 1-3 in the book.)

## A Definition of Causal Effect

First, let's explicate the implicit assumptions when making causal inference. Vilation of these assumptions may induce improper causal inference of any intervention of interest.

1. *No Interference:* An individual's outcome is not influenced by their social interaction with other population members.
    - It means that individuals' outcomes ought to be independent of each other in the presence of intervention of interest.
    - In social networking experiments/obsevational studies, this assumption is unlikely to hold.
2. *Treatment Variation Irrelevance:* Multiple versions of treatment may exist but they all result in the same counterfactual outcome.
    - It means that the intervention should be well-defined and -measured.

For simplicity, we assume that the outcome $Y^{a}$ is a dichotomous variable that takes on one of only two possible values when observed or measured. Now with the assumptions made, for a given intervention $A=a$, what is the definition of average causal effect?

We state that the null hypothesis of no average causal effect is $E[Y^{a=1}]=E[Y^{a=0}]$, or equivalently, $E[Y^{a=1}-Y^{a=0}=0]$. Here we only consider the mean statistics, however, if we consider other nonlinear functional statistics, the equation equivalence does not in general hold.

There are three measures of causal effect under the null:

1. Causal risk differece - measuring the absolute number of cases of the outcome attributable to the treatment.
    $$P(Y^{a=1}=1) - P(Y^{a=0}=1) = 0$$

2. Causal risk ratio - measuring how many times treatment relative to no treatment increases the outcome of interest.
    $$\frac{P(Y^{a=1}=1)}{P(Y^{a=0}=1)} = 1$$

3. Causal odds ratio.
    $$\frac{P(Y^{a=1}=1)/P(Y^{a=1}=0)}{P(Y^{a=0}=1)/P(Y^{a=0}=0)} = 1$$

One of the difficulties in measuring the causal effect is that we only observe one of outcomes if the individual is treated or untreated. The counterfactual outcomes under no treatment ($P(Y^{a=0}=1)$) cannot be directly computed. Besides, the counterfactual outcomes are likely nondeterministic, and vary across individuals.

Instead, we define the measures of association under the null as follows:

1. Associative risk difference.
    $$P(Y=1 \vert A=1) - P(Y=1 \vert A=0) = 0$$

2. Associative risk ratio.
    $$\frac{P(Y=1 \vert A=1)}{P(Y=1 \vert A=0)} = 1$$

3. Associative odds ratio.
    $$\frac{P(YY=1 \vert A=1)/P(Y=0 \vert A=1)}{P(YY=1 \vert A=0)/P(Y=0 \vert A=0)} = 1$$

If $P(Y=1 \vert A=1) \neq P(Y=1 \vert A=0)$, treatment $A$ and outcome $Y$ are independent. In other words, for binary treatment $A$, $Y$ and $A$ are not associated if and only if they are not statistically correlated.

So, what indeed is the difference between causal inference and associative inference? Causal inference asks *what if*, what would be the risk if everybody had been treated or untreated? Associative inference quests *reality*, what is the risk in the treated or untreated?

Causation is defined by a different risk in the same population under the two different treatment values, $P(Y^{a}=1)$, $a=1$ or $a=0$. Association is defined by a different risk in two disjoint subsets of the population determined by the individual's actual treatment value, $P(Y=1 \vert A=a)$, $A=1$ or $A=0$.

## Randomized Experiments

To make causal inference in randomized experiments, *exchangeability* is required. When the group membership is randomized, which particular group received the treatment is irrelevant for the value of $P(Y=1 \vert A=1)$ and $P(Y=1 \vert A=0)$.

$$ P(Y^{a}=1 \vert A=1) = P(Y^{a}=1 \vert A=0) = P(Y^{a}=1) $$

The counterfactual outcome and the actual treatment are independent, $Y^{a} \perp A$, $\forall a$. It means that the counterfactual risk under treatment value $a$ is the same in both groups $A=1$ and $A=0$. In this case, treatment is exogenous.

$$
\begin{aligned}
P(Y^{a=1}=1) &= P(Y=1 \vert A=1) \\
P(Y^{a=0}=1) &= P(Y=1 \vert A=0)
\end{aligned}
$$

Notice that,  $Y^{a} \perp A$ is different from  $Y \perp A$. The treatment can be associated with the observed outcome.

## Conditional Randomization

In reality, we are unable to determine whether exchangeability holds in our study. 
