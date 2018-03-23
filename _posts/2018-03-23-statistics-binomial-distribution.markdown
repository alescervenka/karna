---
layout: post
title:  "Statistics in R: Binomial Distribution"
description: Let's use the R and RStudio to learn more about the binomial distribution!
date:   2018-03-23 07:3S0:00 +0530
categories: jekyll update
img: board_binom_distribution.jpg
categories: [math]
color: 1976D2
author: alyosha
---

Let's use the R and RStudio to learn more about the binomial distribution!

* TOC
{:toc}

# Downloading the Project

We will be using the ProbabilityDistributions project, which you can download in the form of a ZIP archive [ProbabilityDistributions.zip](https://github.com/alescervenka/pastinak-examples/raw/master/zip/ProbabilityDistributions.zip). After you've downloaded the archive, proceed by extracting it, go into a newly created ProbabilityDistributions folder and double-click on the ProbabilityDistributions.Rproj icon. This opens up the ProbabilityDistributions project in the RStudio.

# Introduction

This entire paragraph was taken over from the Introduction to Statistical Thought (written by Michael Lavine; published on June 24, 2010).

Statisticians often have to consider observations of the following type:

* A repeatable event results in either a success or a failure.
* Many repetitions are observed
* Successes and failures are counted
* The number of successes helps us learn about the probability of success.

Because binomial experiments are so prevalent there is specialized language to describe
them. Each repetition is called a trial; the number of trials is usually denoted N; the
unknown probability of success is usually denoted either _p_ or _θ_; the number of successes
is usually denoted _X_. We write _X ∼ Bin(N, p)  _.
The symbol “∼” is read is distributed as; we
would say “X is distributed as Binomial N p” or “X has the Binomial N, p distribution”.

Some important assumptions about binomial experiments are that _N_ is fixed in advance,
_θ_ is the same for every trial, and the outcome of any trial does not influence the outcome
of any other trial.


# Generating binomial data

Let's create a function _summarize.binomial.observations_, which takes the following parameters:

* trials - a number of trials (_N_)
* theta - a probability of success (_θ_)
* observations - a number of observations to be made

```script
library(tidyverse)

summarize.binomial.observations <- function(trials, theta, observations) {
  sample.space <- c(1,0)
  results <- 1:observations %>%
  map_int(function(x)
    as.integer(
      sum(
        sample(sample.space, size = trials, replace = TRUE, prob = c(theta, 1 - theta))
      )
    )
  )
  return(results)
}
```

Now we can use the function to generate 3000 observations of X ∼ Bin(80, 0.6):

```script
summary <- summarize.binomial.observations(80, 0.6, 3000)
resulting.df <- data.frame(flips <- summary) # ggplot only works with data frames
names(resulting.df) <- c("flips")
#binPDF <- data.frame(x<-1:80, y<-dbinom(1:80, size=80, prob = 0.6))
#names(binPDF) <- c("flips", "prob")

ggplot(resulting.df) + 
  geom_histogram(breaks=seq(1, 80, 2), aes(x=flips, y=..density..), position="identity") + 
  geom_density(aes(x=flips, y = ..density..), colour="red")

```

![binomial probability distribution function]({{site.baseurl}}/images-hq/binom_01.png)

It turns out that R already contains a function which produces the same data as _summarize.binomial.observations_. The function is called _rbinom_ and it repeatedly performs a random draw from a binomial distribution.

```script
drawsV1 <- summarize.binomial.observations(80, 0.6, 3000)
drawsV2 <- rbinom(3000, 80, 0.6)
mean(drawsV1)
mean(drawsV2)
length(drawsV1)
length(drawsV2)
```

produces:

```script
[1] 48.01467
[1] 48.052
[1] 3000
[1] 3000
```

# Probability Density

The probability of observing exactly 5 heads out of 10 flips can be estimated as

```script
mean(rbinom(1000, 10, .5) == 5)
```

result:

```script
[1] 0.232
```

There is a special function in R which calculates the probability density - it is called _dbinom_:

```script
dbinom(5, 10, .5)
```

yields:

```script
[1] 0.2460938
```

# Cumulative Density

The probability of observing exactly at most 4 heads out of 10 flips can be estimated as

```script
mean(rbinom(1000, 10, .5) <= 4)
```

result:

```script
[1] 0.392
```

There is a special function in R which calculates the cumulative density - it is called _pbinom_:

```script
pbinom(4, 10, .5)
```

output:

```script
[1] 0.3769531
```

# Quantiles

Quantile works as an inverse of the cumulative density function, as illustrated below:

```script
qbinom(pbinom(4, 10, .5), 10, .5)
```

```script
[1] 4
```

Visit [Basic Probability Distributions in R](https://rpubs.com/ggraham412/100906) for more information.

# Quantile-Quantile Plots

As described in the [Q-Q Plot Tutorial](https://intellinexus.wordpress.com/2010/11/29/creating-a-q-q-plot/), The quantile-quantile (q-q) plot is a graphical technique for determining if two data sets come from populations with a common distribution.

The following code compares observations stored in _x.sample_ with those in _y.sample_:

```script
x.sample <- rbinom(1000, 19, .5)
y.sample <- rbinom(1000, 19, .5)
qqplot(x.sample, y.sample)
abline(0,1)
```

![qq-plot of binomial data]({{site.baseurl}}/images-hq/binom_qq_01.png)

The same test using _ggplot2_:

```script
nq <- 31
p <- (1 : nq) / nq - 0.5 / nq
ggplot() + geom_point(aes(x = quantile(x.sample, p), y = quantile(y.sample, p))) +
  geom_abline(intercept = 0, slope = 1)
```

![qq-plot of binomial data created with the ggplot2]({{site.baseurl}}/images-hq/binom_qq_02.png)

Do the following to compare the _x.sample_ with a binomial distribution Bin(19, 0.5):

```script
xdf <-data.frame(x = x.sample)
ggplot(xdf, aes(sample = x)) + 
  stat_qq(distribution = stats::qbinom, dparams = list(size = 19, prob=0.5)) + 
  geom_abline(intercept = 0, slope = 1)
```

![qq-plot of a data sample compared to data generated by qbinom]({{site.baseurl}}/images-hq/binom_qq_03.png)

# Further Reading

* [A quantile-quantile plot](http://ggplot2.tidyverse.org/reference/geom_qq.html)
* [QQ Plots and PP Plots](http://homepage.divms.uiowa.edu/~luke/classes/STAT4580/qqpp.html)
* [Q-Q Plot Tutorial](https://intellinexus.wordpress.com/2010/11/29/creating-a-q-q-plot/)