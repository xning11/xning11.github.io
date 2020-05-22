---
title: "First Post Test"
excerpt: "The first post test."
tags: 
  - casual
toc: true
---

Finally, my personal website - I got it running. 

## Test header 2

This is a test... 

### Test header 3 

This is a test... 

1. Statistics
  1. Hypothesis testing 
  2. Experimental design
2. Machine Learning
  1. Supervised 
  2. Unsupervised
3. Software Engineering (including SQL)
4. "Soft" Questions

### Test header 3 

This is a test... 

| Description | Value |
|-------------|-------|
| Null Hypothesis| $$p_{blue} - p_{green} < 0$$ |
| Test Statistic | $$ \frac{k_\text{blue}}{n} - \frac{k_\text{green}}{n} $$ |
| Test Statistic's Distribution | $$N(0, (p_b(1-p_b) + p_g(1-p_g)) / n)$$ |
| Test Statistic's Observed Value | -0.09 |
| $$p$$-value | 0.1003 |

## Test header 2

This is a test... 

### Test header 3 

This is a test... **Test** 

{% highlight python %}
from scipy.stats import norm
pb = 0.48
pg = 0.57
n = 100
sigma = np.sqrt((pb*(1-pb) + pg*(1-pg))/n)
norm.cdf(-0.09, loc = 0, scale = sigma) # 0.10034431272089045
{% endhighlight %}

#### Test header 4 

This is a test... **Test** 

- test 
- test 
  - test 
- test 
    - test 
    - test 
      - test 

## Test header 2 

This is a test...

**Watch out!** You can also add notices by appending `{: .notice}` to a paragraph.
{: .notice}

**Primary Notice:** You can also add notices to a paragraph.
{: .notice--primary}

**Info Notice:** You can also add notices to a paragraph.
{: .notice--info}

> This is a quote.
