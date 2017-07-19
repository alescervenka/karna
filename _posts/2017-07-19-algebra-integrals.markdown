---
layout: post
title:  "Algebra in R: Integrals"
description: Let's use the R and RStudio to integrate elementary functions!
date:   2017-07-19 07:3S0:00 +0530
categories: jekyll update
img: board_derivatives.jpg
categories: [statistics]
color: BF360C
author: alyosha
---

Let's use the R and RStudio to integrate elementary functions!

* TOC
{:toc}

# Pre-Requisites

We will use the RYACAS packacke, which we installed when we studied the [Derivatives](../algebra-derivatives).

# Downloading the Project

We will be using the Integrals project, which you can download in the form of a ZIP archive [Integrals.zip](https://github.com/alescervenka/pastinak-examples/raw/master/zip/Integrals.zip). After you've downloaded the archive, proceed by extracting it, go into a newly created Integrals folder and double-click on the Integrals.Rproj icon. This opens up the Integrals project in the RStudio.

# Determining Integrals

The Integrals project contains only one script, called *01_integrals.R*. It shows how to use the yacas function to determine integrals of elementary functions.

```script
# Constant function
# -----------------

yacas("Integrate(x) 0")

# Linear function
# ---------------

yacas("Integrate(x) 1")
yacas("Integrate(x) 2")

# Polynomial functions
# --------------------

yacas("Integrate(x) x^3")

# Rational functions
# ------------------

yacas("Integrate(x) 1/x")

# Exponential functions
# ---------------------

yacas("Integrate(x) a^x")
yacas("Integrate(x) e^x")

# Trigonometric functions
# -----------------------

yacas("Integrate(x) Sin(x)")
yacas("Integrate(x) Cos(x)")
```
