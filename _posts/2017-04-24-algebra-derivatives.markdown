---
layout: post
title:  "Algebra in R: Derivatives"
description: Let's use the R and RStudio to derive and plot derivatives of elementary functions!
date:   2017-04-24 07:3S0:00 +0530
categories: jekyll update
img: board_derivatives.jpg
categories: [statistics]
color: 00897B
author: alyosha
---

Let's use the R and RStudio to derive and plot derivatives of elementary functions!

* TOC
{:toc}

# Introduction

I higly recommend going through the [Differential Calculus](https://www.khanacademy.org/math/differential-calculus/derivative-intro-dc/intro-to-diff-calculus-dc/v/newton-leibniz-and-usain-bolt) course at the Khan Academy. The course does a great job at explaining that the derivative represents an instantaneous rate of change.

# Installing YACAS and Ryacas

YACAS (*Yet Another Computer Algebra System*) is a computer algebra system and I will use it in this post to determine derivatives of elementary functions. And because I will be using it from within the RStudio, I will not only need to install the YACAS as such but you need to install the Ryacas plugin as well. The Ryacas is an R plugin which makes it possible for you to call YACAS functions in your R code.

First off, download the YACAS from its [download page](http://www.yacas.org/getting_started/downloads/) and follow installation instructions pertinent to your operating system. This is what I had to do on my Ubuntu 16.04:

```script
wget https://github.com/grzegorzmazur/yacas/releases/download/v1.6.1/yacas-common_1.6.1-1xenial1_all.deb
wget https://github.com/grzegorzmazur/yacas/releases/download/v1.6.1/yacas-doc_1.6.1-1xenial1_all.deb
wget https://github.com/grzegorzmazur/yacas/releases/download/v1.6.1/yacas-console_1.6.1-1xenial1_amd64.deb
sudo dpkg --install yacas-common_1.6.1-1xenial1_all.deb yacas-console_1.6.1-1xenial1_amd64.deb yacas-doc_1.6.1-1xenial1_all.deb
```

Now that the YACAS has been installed, we can move on to installing the Ryacas plugin. On my Ubuntu 16.04, I had to install libxml2-dev first:

```script
sudo apt-get install libxml2-dev
```

This step (libxml2-dev) likely does not apply to you if you run another operating system.

Start the RStudio and swith to the *Packages* tab. When you are there, click on the *Install* button, which brings up an *Install Packages* dialogue window. Type *Ryacas* into the *Packages* text box and click on the *Install* button. 

# Downloading the Project

We will be using the Derivatives project, which you can download in the form of a ZIP archive [Derivatives.zip](https://github.com/alescervenka/pastinak-examples/raw/master/zip/Derivatives.zip). After you've downloaded the archive, proceed by extracting it, go into a newly created Derivatives folder and double-click on the Derivatives.Rproj icon. This opens up the Derivatives project in the RStudio.

# Determining Derivatives

The Derivatives project contains only one script, called *01_derivatives.R*. It shows how to use R's D function as well as the yacas function to determine derivatives of elementary functions. 

## Constant functions

Try 

```script
D(expression(6), "x")
```

and you'll get 0.

## Linear functions

Try 

```script
D(expression(6 * x), "x")
```

and you'll get 6.

You need to do the following to do the same with Ryacas

```script
xx <- Sym("xx")
yacas(deriv(6*xx, xx))
```

## Polynomial functions

Try 

```script
D(expression(x^4 + x^3 + x^2), "x")
yacas(deriv(xx^4 + xx^3 + xx^2, xx))
```

to get _4 * x^3 + 3 * x^2 + 2 * x_.

## Trigonometric functions

Try

```script
D(expression(sin(x)), "x")
yacas(deriv(sin(xx), xx))
```

to get _cos(x)_.

## Exponential functions

Try 

```script
D(expression(5^x), "x")
yacas(deriv(5^xx, xx))
```

to get _5^x * log(5)_.

## Logarithmic functions

Try 

```script
# derivative of y = ln(x)
yacas("D(x)Ln(x)")
```

to get _1/x_.

# Plotting Derivatives

Do the following in order to plot a sine function and its derivative:

```script
curve(sin(x), -8, 8, col = "tan4", ylim = c(-2, 2))
curve(eval(D(expression(sin(x)), "x")), -8, 8, add = TRUE, col = "blue1")
abline(h = 0, v = 0)
```

You could do the same with Ryacas:

```script
curve(sin(x), -8, 8, col = "tan4", ylim = c(-2, 2))
xx <- Sym("xx")
my_deriv <- yacas(deriv(sin(xx), xx))
my_deriv2 <- function(xx) {
  eval(parse(text = my_deriv$text))
}
curve(my_deriv2(x), -8, 8, add = TRUE, col = "blue1")
abline(h = 0, v = 0)
```

Both approaches produce the following plot:

![sin and its derivative]({{site.baseurl}}/images-hq/derivatives_sine.jpeg)

# Further Reading

* [Using R as a Computer Algebra System with Ryacas](https://www.r-bloggers.com/using-r-as-a-computer-algebra-system-with-ryacas/amp/)
* [https://cran.r-project.org/web/packages/Ryacas/vignettes/Ryacas.pdf](https://cran.r-project.org/web/packages/Ryacas/vignettes/Ryacas.pdf)
* [https://cran.r-project.org/web/packages/Ryacas/Ryacas.pdf](https://cran.r-project.org/web/packages/Ryacas/Ryacas.pdf)



{::comment}
http://gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/
https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
{:/comment}