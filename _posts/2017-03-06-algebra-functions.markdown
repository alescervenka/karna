---
layout: post
title:  "Algebra in R: Functions"
description: Let's use the R and RStudio to plot functions and figure out what influences shapes of their graphs!
date:   2017-03-06 07:3S0:00 +0530
categories: jekyll update
img: board_functions.jpg
categories: [statistics]
color: 1976D2
author: alyosha
---

Let's use the R and RStudio to plot functions and figure out what influences shapes of their graphs!

* TOC
{:toc}

# Downloading the Project

We will be using the Functions project, which you can download in the form of a ZIP archive [Functions.zip](https://github.com/alescervenka/pastinak-examples/raw/master/zip/Functions.zip). After you've downloaded the archive, proceed by extracting it, go into a newly created Functions folder and double-click on the Functions.Rproj icon. This opens up the Functions project in the RStudio.

# Linear Functions

```script
constFun <- function(x) rep(3, length(x))
curve(constFun, -1, 6)
```

```script
curve(2*x + 1, -1, 6)
```

# Absolute Value Functions

```script
curve(2*abs(x) + 1, -6, 6)
```

# Quadratic Functions

```script
standardFun <- function(x) 4*(x^2) - 3*x + 5
curve(standardFun, -10, 10)
```

# Linear Rational Functions

```script
curve((3*x + 6)/(2*x + 8), -100, 100)
abline(h = 0, v = 0)
```

# Functions with Rational Exponents

```script
curve(x^(2/3), -2, 4, ylim = c(-1, 8))
```

# Exponential and Logarithmic Functions

```script
curve(3^x, -10, 10, ylim = c(-15, 15))
```

```script
curve(log(x, 3), -10, 10, ylim = c(-5, 5))
```

# Trigonometric Functions

\\[ sin(x^2) \\]

```script
curve(sin(x), -8, 8, col = "tan4", ylim = c(-2, 2))
curve(cos(x), -8, 8, add = TRUE, col = "blue1")
abline(h = 0, v = 0)
```

```script
curve(tan(x), -4, 4, col = "tan4", ylim = c(-2, 2))
curve(1/tan(x), -4, 4, add = TRUE, col = "blue1")
abline(h = 0, v = 0)
```

{::comment}
http://gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/
{:/comment}