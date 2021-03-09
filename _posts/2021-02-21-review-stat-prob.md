---
title: "Review of Statistics, Probability Theory, and Hypothesis Testing"
categories:
  - statistics
tags:
  - statistics 
  - hypothesis testing
toc: true
toc_sticky: true
---

## Priors 

**Statistics** is a mathematical science pertaining to the collection, analysis, interpretation or explanation, and presentation of data. 

**Population** is a representation of all the possible outcomes or measurements of interest. 

**Sample** is any subset of a population of interest to be measured. 

Objective of statistics is to make **statistical inferences** about a population based on information obtained from a representative sample. 

**Parameter** is a numerical summary of a population, typically unknown.

**Statistic** is a numerical summary based on a sample from a population, typically estimated from sample data. 
	
**Common data collection (survey) bias**:
- Sampling - nonrandom samples or under-representative samples, etc.
- Nonresponse - certain subjects don't respond, possible for a reason. 
- Response - incorrect responses (typically lies), vague questions, leading questions, poorly trained investigators, etc. 

**Descriptive/summary statistics**: 
- Relative frequency statistics: mode 
    - Properties: unimodal, multimodal, or non-exist
- Rank-based statistics: quartiles, median, range, IQR
    - Properties: median is more robust to outliers 
- Averaging statistics: mean 
    - Properties: sensitive to outliers, skewed data
- Data variable histogram 
    - Shape (symmetric, skewed, thin/thick tails) 
        - Right-skewed if mean >> median, reflecting a long upper/right tail
		- Left-skewed if mean << median, reflecting a long lower/left tail 
    - Modality (unimodal, multimodal) 
	- Center (mean, median, mode/s)
	- Spread (range, interquartile range, variance), anomaly (outliers), etc.
	    - Deviation - difference between the observation and the mean, sensitive to outlier. 
		- For bell-shaped data, approx. 95% of the measurements fall within 2 std. dev. of the mean; thus, 4 std. dev. nearly covers the range of the data. 
		- A quick (and dirty) approx. for standard deviation is therefore $s=range/4$.

<!-- 
| Parameter	| Statistic | 
| -- | -- |
| $\mu = 1/N \sum_i \mu_i$ <br> (true population mean) | $\bar{y} = 1/N \sum_i y_i$ <br> (sample mean, estimates of $\mu$) | 
| $\sigma^2 = 1/N \sum_i (\mu_i - \mu)^2$ <br> (true population variance) | $s^2 = 1/(N-1) \sum_i (y_i - \bar{y})^2$ <br> (sample variance, estimates of $\sigma^2$) | 
| $\pi = P(y=1)$ <br> (true population proportion) | $\hat{\pi} = y/n$ <br> (sample proportion, estimates of $\pi$) |  
-->


A **random variable** is a numerical measure for outcomes of an event that are not known with certainty beforehand. 
- Discrete random variables 
- Continuous random variables 

A sample of $n$ measurements selected from a population is said to be a **random sample** if every different sample of size $n$ from the population has an equal probability of being selected. 

**Sampling distribution** is the probability distribution of a statistic, depending on the size of the sample and distribution of the population.

**Standard error** is the standard deviation of a statistic, which measures amount of the expected variability in statistic from sample to sample with fixed $n$. 

**Confidence intervals** are range of one margin of error above/below the point estimate. 

$$\text{Conf. interval} = \theta \pm MOE = \theta \pm [c.v. * s.e.]$$
	
A **probability distribution** describes the random behavior of the random variable by specifying all the possible values for the random variable along with the probability of that value occurring. 

A **probability density function** is a graph of a continuous probability distribution that satisfies the following two properties:
- The total area under the curve must be 1. 
- Every point on the curve must have a vertical height that is 0 or greater. 

**Normal distribution**
- Bell-shaped, symmetric, approx.
  - 68% of the observations are within the interval $\mu \pm \sigma$
  - 95% of the observations are within the interval $\mu \pm 2\sigma$
  - 99.7% of the observations are within the interval $\mu \pm 3\sigma$
- Probability density function 

$$
f(y)=\frac{1}{\sqrt{2\pi} \sigma} \exp⁡ \left[− \frac{(y−\mu)^2}{2\sigma^2}\right]
$$


**Binary distribution** 
- Two outcomes
  - With prob $P(y=1)=\pi$ or $P(y=0)=1−\pi$
  - Mean of $\mu=\pi$ and $\sigma=\sqrt{\pi(1-\pi)}$  

**Binomial distribution**
- Represents number of successes in $n$ independent and identical binary trails, with prob of success $\pi$
  - Mean of $\mu=n\pi$ and $\sigma=\sqrt{n\pi(1-\pi)}$  
- Probability mass function 

$$
P(Y=y)= {n \choose y} \pi^y (1−\pi)^{n−y} 
$$


**Normal approximation to the Binomial** 
- If $n \pi \geq 5$ and $n(1−\pi) \geq 5$, then the distribution of $y$ can be approximated by the Normal distribution with mean $n\pi$ and std $\sqrt{n\pi(1-\pi)}$. 

$$
y \sim Binomial(n, \pi)
$$

- Normal approx. to Binomial is very accurate when $n\pi \geq20$ and $n(1−\pi)\geq20$

$$
\begin{aligned}
y &\mathrel{\dot\sim} N(n \pi,n \pi(1− \pi)) \\
z &= \frac{y−n\pi}{n\pi(1−\pi)} \sim N(0,1)
\end{aligned}
$$


## Central Limit Theorem

Under certain restrictions, given a sequence of independent and identically-distributed random variables, $\{X_1, X_2, ..., X_n\}$, with the same mean $\mu$ and standard deviation $\sigma$. Let $\bar{X}_n$ be the average of $X_1, X_2, ..., X_n$:
$$\bar{X}_n = \frac{1}{n} \sum_i X_i$$
which is itself a random variable. The law of large numbers and central limit theorem tell us about the value and distribution of $\bar{X}_n$, respectively. 

- **LoLN**: As $n$ increases, the probability that $\bar{X}_n$ is close to $\mu$ goes to 1. 
- **CLT**: As $n$ increases, the distribution of $\bar{X}_n$ converges to the Normal distribution, $N(\mu, \sigma^2/n)$.


### Application under CLT

The **sampling distribution of mean $\bar{y}$** approaches the Normal distribution as $n$ increases

$$
\begin{aligned}
\bar{y} &\mathrel{\dot\sim} N \left(\mu, \frac{\sigma}{\sqrt{n}}\right)    \\
z &= \frac{\bar{y}-\mu}{\sigma / \sqrt{n}} \sim N(0,1)  
\end{aligned}$$

- If sample from a normal population, the sampling distribution of $\bar{y}$ is Normal regardless of the size of $n$.

$\sigma$ is a population parameter, usually unknown; empirically we replace $\sigma$ with $s$, use $t$-score instead of $z$-score. 

$$
t = \frac{\bar{y} - \mu}{s/\sqrt{n}} \mathrel{\dot\sim} t_{n−1}
$$

- Student's $t$ distribution usually has fatter tails than Normal distribution. When sample size $n$ increases, they become more consistent. 
  
A $100(1−\alpha)\%$ Conf. Interval for $\mu$ (the population mean) is given by 

$$
\bar{y} \pm t_{[n−1, \alpha/2]} \cdot \left( \frac{s}{\sqrt{n}}\right)
$$

Minimum sample size $n$ needed to achieve a $100(1−\alpha)\%$ Conf. Interval with margin of error $m$, is derived as follows

$$
n \geq \frac{(z_{\alpha/2})^2 \sigma^2}{m^{2}} 
$$

which requires a preliminary assessment of $\sigma$, a desired confidence level $\alpha$, and a required margin of error $m$.
- Here assumes $\sigma$ is known, empirical rule: $\sigma \approx range/4$
- When $\sigma$ is unknown, the $t$-distribution must be used. 


The **sampling distribution of proportion $\hat{\pi}$** is roughly Normal as long as $n$ is "large enough" ($n\pi\geq 5$ and $n(1−\pi)\geq 5$). 

$$
\hat{\pi} \mathrel{\dot\sim} N \left(\pi, \sqrt{\frac{\pi(1-\pi)}{n}}\right)
$$

A $100(1−\alpha)\%$ Conf. Interval for $\pi$ (the population proportion) is given by 

$$
\hat{\pi} \pm z_{\alpha/2} \cdot \left(\sqrt{\frac{\hat{\pi}(1-\hat{\pi})}{n}}\right)
$$

Minimum sample size $n$ needed to obtain a $100(1−\alpha)\%$ Conf. Interval with margin of error $m$ for the proportion $\pi$ of the population, is derived as follows

$$
n \geq \frac{(z_{\alpha/2})^2 \pi (1-\pi)}{m^2}
$$

which requires a preliminary assessment of $\pi$.


## Hypothesis Testing

**Hypothesis Testing** is a detailed protocol for decision-making concerning a population by examining a sample from that population. 

**Significance level** is the level, denoted by $\alpha$, at which we are willing to start rejecting the null hypothesis $H_0$. 

**Type I error** is the error committed when the true null hypothesis $H_0$ is rejected.  
    $$P(\text{type I error})=\alpha$$

**Type II error** is the error that fails to reject the null hypothesis $H_0$  when the alternative hypothesis $H_a$ is true. 
$$P(\text{type II error})=\beta$$

**Power** is the probability of rejecting the null hypothesis $H_0$ when it is false.  
$$\text{power} = 1−\beta$$
- The power of a hypothesis test is the probability to detect a specified difference in the means when that difference exists. 
- Power depends on $\mu_1 - \mu_0$, $\alpha$, $\sigma^2$ and $n$. 

A **p-value** is the probability under the null hypothesis of obtaining a point estimate as "extreme" or more "extreme" than would be observed by chance along, where the definition of "extreme" is taken from the alternative hypothesis (i.e., observing your sample results or more extreme results) assuming the null hypothesis is true. 
- If $p$-value is small, either $H_0$ is true and we have observed a rare event, or $H_0$ is false. 

**Rejection rule**: reject the null hypothesis $H_0$ if the $p$-value $\leq \alpha$.

**Procedures**:
- State assumptions of the population distribution from which the sample is drawn
- Determine the null and alternative hypotheses (one-sided, two-sided)
- Specify significance level $\alpha$
- Calculate the observed value of the test statistic
- Calculate the $p$-value or critical value 
- Check assumptions, e.g., sample size large enough for applying CLT 
- Draw conclusion according to rejection rule. 
	
**One-sample, two-sample, and paired tests**: 
- One-sample $t$ test is used to measure whether the mean of a sample is far from a preconceived population mean. 
- Two-sample $t$ test is used to measure whether the difference in sample means between two groups is large enough to substantiate a rejection of the null hypothesis that the population means are indifferent across the two groups. 
- Paird $t$ test is used to measure individual level variation, i.e., test for whether the per-individual differences are large enough to reject the null hypothesis of zero differences. 


### Two-sample $t$ tests for means 

Two samples of sizes $n_1$ and $n_2$, independently drawn from separate populations with means $\mu_1$ and $\mu_2$ and variances $\sigma_1^2$ and $\sigma_2^2$.

$$H_0: \mu_1 = \mu_2,   \quad   H_a: \mu_1 \neq \mu_2$$  

The sampling distribution of the difference between sample means 

$$
\begin{aligned}
\bar{y}_1 - \bar{y}_2 &\sim N \left(\mu_1 - \mu_2, \sqrt{\frac{\sigma_1^2}{n_1}+\frac{\sigma_2^2}{n_2}}\right) \\ 
Z &= \frac{(\bar{y}_1 - \bar{y}_2) - (\mu_1 - \mu_2)}{\sqrt{\frac{\sigma_1^2}{n_1}+\frac{\sigma_2^2}{n_2}}} \sim N(0,1)    
\end{aligned}
$$

In practice, $\sigma_1$ and $\sigma_2$ are likely unknown, replace by $s_1$ and $s_2$.
  - Rule of thumb: consider the variances different if the ratio of larger to smaller variance is more than four, i.e., $\frac{s_{max}^2}{s_{min}^2} > 4, \quad \text{or} \frac{s_{max}}{s_{min}}>2$

If we can assume $\sigma=\sigma_1=\sigma_2$, then

$$\sqrt{\frac{\sigma_1^2}{n_1}+\frac{\sigma_2^2}{n_2}} = \sigma \sqrt{\frac{1}{n_1}+\frac{1}{n_2}} $$

Estimate this common $\sigma$ by pooling the data 

$$s_p = \sqrt{\frac{(n_1 - 1)s_1^2+(n_2 - 1)s_2^2}{n_1 + n_2 - 2}}$$

The pooled $t$-test statistic is 

$$t = \frac{\bar{y}_1 - \bar{y}_2}{s_p \sqrt{\frac{1}{n_1}+\frac{1}{n_2}}} $$

For independent random samples drawn from normal populations, when $\sigma_1$ and $\sigma_2$ are unknown but $\sigma_1 \approx \sigma_2$, a $100(1−\alpha)\%$ conf. interval for $\mu_1−\mu_2$ is 

$$\bar{y}_1 - \bar{y}_2 \pm t_{[n_1+n_2−2,\alpha/2]} \cdot \left(s_p \sqrt{\frac{1}{n_1}+\frac{1}{n_2}}\right)$$

If $\sigma_1$  and $\sigma_2$ are completely unknown, then  

$$s_{\bar{y}_1 - \bar{y}_2} = \sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}}$$

The statistic is NOT a $t$ random variable, NOR a standard normal random variable. It has a modified $t$ distribution (Welch's $t$-test) with modified degrees of freedom (truncated to the nearest integer) 

$$df_S =  \frac{\left(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}\right)^2}{\left(\frac{s_1^2}{n_1}\right)^2 /(n_1 -1) + \left(\frac{s_2^2}{n_2}\right)^2 /(n_2 -1)}, \quad  df_S \leq n_1+n_2−2$$

For independent random samples drawn from normal populations, when $\sigma_1$ and $\sigma_2$ are unknown, a $100(1−\alpha)\%$ conf. interval for $\mu_1−\mu_2$ is 

$$\bar{y}_1 - \bar{y}_2 \pm t_{[df_S, \alpha/2]} \cdot \left(\sqrt{\frac{s_1^2}{n_1}+\frac{s_2^2}{n_2}}\right)$$

Pooled $t$ test is more powerful (i.e., more likely to reject a wrong $H_0$) when $\sigma_1=\sigma_2$ is true. 
Welch's $t$ test is more reliable when  $\sigma_1 \neq \sigma_2$, but more conservative. 


### Paired $t$ test for mean differences

Each sample has the same number of observations $n=n_1=n_2$, observations are naturally paired, thus, NOT independent. 

Only interested in the difference $d_i=y_{1i}−y_{2i}$ between each pair. 

$$H_0: d = \mu_{y1} - \mu_{y2} = 0,   \quad   H_a: d \neq 0$$  

Sample mean for differences is

$$\bar{d} = \frac{1}{n} \sum_i d_i = \bar{y}_1 - \bar{y}_2 $$

Sample standard error for differences is

$$s_D = \sqrt{\frac{\sum_i (d_i - \bar{d})^2}{n-1}}$$

The paired $t$ test statistic is 

$$t = \frac{\bar{y}_1 - \bar{y}_2}{s_D/\sqrt{n}}$$

For independent random samples drawn from normal populations, when the data naturally pair, a $100(1−\alpha)\%$ conf. interval for $\mu_1−\mu_2$ is 

$$\bar{y}_1 - \bar{y}_2 \pm t_{[n−1, \alpha/2]} \cdot \left(\frac{s_D}{\sqrt{n}} \right)$$


### Two-sample $z$ test for proportions 

Two samples of sizes $n_1$ and $n_2$, independently drawn from separate populations with proportions $\pi_1$  and $\pi_2$.

$$H_0: \pi_1 = \pi_2,  \quad  H_a: \pi_1 \neq \pi_2 $$

The sampling distribution of proportion difference  

$$
\begin{aligned}
\hat{\pi}_1 − \hat{\pi}_2 &\sim N \left(\pi_1−\pi_2,\sqrt{\frac{\pi_1(1-\pi_1)}{n_1} + \frac{\pi_2(1-\pi_2)}{n_2}}\right) \\ 
Z &= \frac{\hat{\pi}_1 - \hat{\pi}_2}{\sqrt{\frac{\pi_1 (1-\pi_1)}{n_1}+ \frac{\pi_2 (1-\pi_2)}{n_2}}} \sim N(0,1)    
\end{aligned}
$$

For independent random samples drawn from binary populations, $n_1 \pi_1\geq 5$, $n_1 (1−\pi_1)\geq 5$, $n_2 \pi_2\geq 5$, $n_2 (1−\pi_2)\geq 5$, a $100(1−\alpha)\%$ conf. interval for $\pi_1−\pi_2$ is 

$$\hat{\pi}_1 - \hat{\pi}_2 \pm Z_{[\alpha/2]} \cdot \left(\sqrt{\frac{\hat{\pi}_1 (1-\hat{\pi}_1)}{n_1}+ \frac{\hat{\pi}_2 (1-\hat{\pi}_2)}{n_2}} \right)$$
		

## Analysis of Variance (ANOVA) 

One-way ANOVA is used to test if the response mean is independent of the treatment or if there is some association present. 

Two-way ANOVA is used to test whether either of two factors, or their interaction, are associated with some continuous response.


###**One-way ANOVA**

Let there be $T$ groups where each group has $n_t$ number of samples selected from population $t$, each with population mean $\mu_1, \mu_2, ...,\mu_T$, the total number of samples is $N=\sum_t^T n_t$. Then a question of interest is whether or not all the means are equal. 

$$H_0: \mu_1 = \mu_2 = ... = \mu_T,  \quad  H_a: \text{At least one mean differs} $$


There are two types of variability:
- Variability between group means $(\bar y_{t}. = \sum_i^{n_t} y_{ti}/n_t)$ around the overall mean $(\bar y.. = \sum_t^T \sum_i^{n_t} y_{ti}/N)$
- Variability within each group $(y_{ti})$ around the group mean $(\bar y_{t}. = \sum_i^{n_t} y_{ti}/n_t)$

As a result, the larger the group to group variability, i.e., the further $\bar{y}_{t}.$ falls from $\bar{y}..$, the more likely there are differences in the true means. 

The larger the variability within groups, i.e., the more the individual $y_{ti}$ vary around $\bar{y}_{t}.$, the harder it is to determine if any difference we see is really significant. 

The **between-sample variability** is measured by the sum of squared deviations between samples:

$$
\begin{aligned}
  SSB &= \sum_t^T n_t (\bar{y}_{t}. - \bar{y}..)^2 \\
      &= \sum_t^T n_t (\bar{y}_{t}.)^2 - N (\bar{y}..)^2 
\end{aligned}
$$

- If $H_0$ is true, we expect $\bar y_{1}. \approx ... \approx \bar y_{t}. \approx \bar y..$ resulting in $SSB \approx 0$.
- If $H_a$ is true, we expect $SSB > 0$. 

*Mean square between samples* is defined as an estimate of sample-to-sample variability based on how different the means from each group are from the grand mean. 

$$MSB = s_B^2 = \frac{SSB}{T-1}$$ 

The **within-sample variability** is measured by the sum of squared errors: 

$$
\begin{aligned}
  SSE &= \sum_t^T \sum_i^{n_t} (y_{ti} - \bar{y}_{t}.)^2 \\
      &= \sum_t^T \sum_i^{n_t} (y_{ti})^2 -  \sum_t^T n_t (\bar{y}_{t}.)^2 
\end{aligned}
$$

*Mean square error* is defined as an estimate of average variability within each group. 

$$MSE = s_E^2 = \frac{SSE}{N-T}$$ 

Note that the sample total variability $(SST)$ is the sum of between- and within- variance. 

$$
\begin{aligned}
  SST &= \sum_t^T \sum_i^{n_t} (y_{ti} - \bar{y}..)^2 \\
      &= \sum_t^T \sum_i^{n_t} (y_{ti} - \bar{y}_{t}. + \bar{y}_{t}. - \bar{y}..)^2 \\
      &= \sum_t^T \sum_i^{n_t} (y_{ti})^2 - N (\bar{y}..)^2 \\
      &= SSB + SSE 
\end{aligned}
$$

Under $H_0$ and assuming equal variances for all sample groups, both $s_B^2$ and $s_E^2$ are unbiased estimates for the random error $\sigma^2$. When $H_0$ is not true, $s_E^2$ is still an unbiased estimates of $\sigma^2$ but $s_B^2$ is a biased, inflated estimate of $\sigma^2$. So if the samples really do have different means we would observe $s_B^2 > s_E^2$.

**Assumptions under ANOVA**:
- Independent groups, random sampling 
- Common variance across all groups (homoskedasticity)
- Population distribution for each group is approximately Normal. 

We use $F$-test statistic to compare the between-sample variability with the within-sample variability, 

$$F_{\text{obs}} = \frac{SSB/(T-1)}{SSE/(N - T)} = \frac{s_B^2}{s_E^2} = \frac{MSB}{MSE}$$

which follows an $F$ distribution with $df_1 = T-1$ and $df_2 = N-T$, under $H_0$ and assuming homoskedasticity. $F$-score is also called "signal-to-noise" ratio. 

We reject $H_0$ if $F_{\text{obs}} > F_{[T-1, N-T, \alpha]}$ or if $p$-value $\leq \alpha$. 


**Checking ANOVA Assumptions**

When the samples are balanced or nearly balanced ANOVA is robust to homoskedasticity assumption, i.e., ANOVA works well even if there is a severe problem of heteroskedasticity. 

- Rule of thumb: if $\frac{s_{max}}{s_{min}} \leq 2$ then it can be assumed that the variances of each group are approx. equal. 
- Check the data using the residuals vs. predicted graph. 

When the graphical methods show extreme skew in samples, it may violate normality assumption. 

- Use normal quantile plot to check whether or not a dataset is approx. normally distributed. Departures from the line indicate departures from normality. 


###**Post-ANOVA Analysis**

If we have rejected $H_0$ and claim that at least one group mean differs from others, what comes next? We need to explore the actual differences and detect in which group(s) they exist. Contrasts and Multiple Comparisons are often used as a post-ANOVA analysis, though they can be done without doing an ANOVA first.  

A **contrast** represents a linear combination of comparisons among group or population means that you are interested in. 

$$H_0: l = 0 \quad  H_a: l\neq 0$$

Generic contrast forluma is written as: 

$$
l = \sum_t a_t \mu_t \quad \text{where} \sum_t a_t = 0 
$$

Estimated contrast formula is obtained by replacing the group means with their point estimates:

$$
\hat{l} = \sum_t a_t \bar{y}_t. \quad \text{where} \sum_t a_t = 0 
$$

Under the ANOVA assumptions, $\hat{l}$ is a linear combination of group means, independent normal random variables, so $\hat{l}$ must also be normal. 

The estimated standard error for $\hat{l}$ is 

$$
s_{\hat{l}} = \sqrt{\sum_t a_t^2 s_{\bar{y}_t.}}  = \sqrt{\sum_t a_t^2 \frac{MSE}{n_t}} 
$$

The standardized $\hat{l}$ is distributed as a $t$-distribution with $N-T$ degrees of freedom:

$$
\frac{\hat{l} - l}{\sqrt{MSE \sum_t \frac{a_t^2}{n_t}}} \mathrel{\dot\sim} t_{[N-T,\alpha/2]} 
$$

where 

$$
MSE = s_E^2 = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2 + \cdots + (n_T -1)s_T^2}{N-T}
$$

Under the null hypothesis, a $100(1−\alpha)\%$ conf. interval for contrast is 

$$
\hat{l} \pm t_{[N-T,\alpha/2]} \cdot \left( \sqrt{MSE} \sqrt{\sum_t \frac{a_t^2}{n_t}} \right)
$$


**Multiple Comparisons** methods are used to preserve the statistical validity of inferences when more than one inference is to be made on the same dataset. 

When conducting multiple comparisons, we first need to set the experiment-wise type I error ($\alpha_E$) to control for overall error rate for all tests, then determine the individual-comparison-wise type I error ($\alpha_I$) to control for error rate for each single test. In other words, we need to control for the type I error for the whole experiment (of multiple tests) rather than for each individual test. 

To see this, say we conduct 20 simultaneous tests, what is the probability of at least observing one significant result (under the null hypothesis that none of the tests are significant)? 

$$
\begin{aligned}
  P(\text{making an error in one test}) &= \alpha_I \\ 
  P(\text{not making an error in one test}) &= 1 - \alpha_I \\ 
  P(\text{not making any error in $m$ tests}) &= (1 - \alpha_I)^m \\ 
  P(\text{making at least an error in $m$ tests}) &= \alpha_E = 1 - (1 - \alpha_I)^m 
\end{aligned}
$$

We have a $[1 - (1 - 0.05)^{20}] \approx 64\%$ change of observing at least one significant result for a set of 20 tests, even if all of the tests are actually not significant (under the null). 

There are a few methods to correct for multiple testing. The **Bonferroni correction** sets the experiment-wise significance level at $\alpha_E = \alpha_I /m$. In this case, the probability of observing at least one significant result is 

$$
\begin{aligned}
  P(\text{at least one significant result}) &= 1 - P(\text{no significant results}) \\
   &= 1 - (1 - \frac{\alpha_I}{m})^m \\ 
   &= 1 - (1 - \frac{0.05}{20})^{20} \\
   &\approx 0.0488 
\end{aligned}
$$

The Bonferroni correction is a single-step method, it relies on the assumption that all tests are independent. Depending on the actual correlation structure of the tests, the Bonferroni correction can be very conservative, leading to a high false negative rate (the type II error). In other words, it fails to reject more often than expected when a difference actually exists in the means especially when there are a lot of groups. 


<details>
<summary><i> Click here for other correction methods used in multiple testing.</i></summary>

A similar method, called **Holmes-Bonferroni correction**, is a sequential procedure. After all tests have been performed, we sort all unadjusted $p$-values with the most extreme one (the lowest type I error rate) being the first, $p_1 \leq p_2 \leq ... \leq p_m$. Starting from $i=1$, we compare $p_i$ and $\alpha/(m-i+1)$, reject the null hypothesis $H_i$ if and only if $p_i \leq \alpha/(m-i+1)$. The Holmes method is less conservative than the Bonferroni method and thus has more statistical power. 

Another approach proposed by Benjamini and Hochberg is to control for the **false discovery rate (FDR)**, which is defined as the proportion of false positives among all significant results (where the null has been rejected). The idea is that for larger $m$ tests, we do not expect all of the null hypotheses to be true, and so we do not want to restrictively control false positives (the type I error). Instead, we want to control the expected rate of false positive discoveries assuming we make at least one discovery. 

To control FDR at level $\delta$, we sort the unadjusted $p$-values with the smallest being the first, we compare and reject the null hypothesis $H_j$ if and only if $p_j \leq \delta \cdot j/m$. 

Storey's Method is to estimate **positive FDR**, using Storey $q$-value, whih is a function of the $p$-value of an individual test and the distribution of the $p$-values for all the tests performed. It reflects the proportion of test results (discoveries) that are likely to be false positives (false discoveries) for a given $p$-value in a given set of tests. 

</details>

