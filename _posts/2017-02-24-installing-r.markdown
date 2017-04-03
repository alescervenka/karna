---
layout: post
title:  "RStudio: A Walkthrough"
description: I'm gonna use the R and RStudio a lot in the subsequent posts, which is why I would first like to demonstrate how to install and use these extremely useful tools.
date:   2017-02-25 07:3S0:00 +0530
categories: jekyll update
img: installing-r-01.jpg
categories: [statistics]
color: 43A047
author: alyosha
---

I'm gonna use the R and RStudio a lot in the subsequent posts, which is why I would first like to demonstrate how to install and use these extremely useful tools.

* TOC
{:toc}

# The R

The RStudio depends on the R package, which is why you should download and install R first before moving on to installing the studio.

## Ubuntu

In Ubuntu, all you need to do in order to download and install R and its dependencies is

```script
sudo apt-get install r-base
```

## Other Operating Systems

If you have Windows, Mac OS X or just a different distribution of Linux, follow instructions in the [Download and Install R](https://cran.rstudio.com/) section of the RStudio website.

# The RStudio

## Download

The RStudio Desktop can be downloaded from the [RStudio home page](https://www.rstudio.com/products/rstudio/download/). As described [here](https://www.rstudio.com/products/rstudio/#Desktop), the free version has the same features as the paid version but comes with a different lincense (AGPL) and without support.

If you decide to go with the free version, click on the *Download* button located at the bottom of the FREE column and focus on the *Installers* section of the download page. There you should pick  an installer that is pertinent to your operating system -- there is an EXE installer for Windows, DMG for Mac OS X, DEB package for Ubuntu/Debian and RPM for Fedora/RedHat/openSUSE. 

## Installation

Run the installer. When it completes, start the RStudio Desktop so that you can inspect it's user interface. 

# Working with Projects

Download the [Functions.zip](https://github.com/alescervenka/pastinak-examples/raw/master/zip/Functions.zip) archive --it contains a sample project which we will use in this section to describe various tabs of the RStudio. After the archive has been downloaded, extract it, go into a newly created Functions folder and double-click on the Functions.Rproj icon. This opens up the Functions project in the RStudio.

![Files Tab]({{site.baseurl}}/images-hq/rstudio_files.png)

On the _Files_ tab in the bottom-right corner of the window (indicated with red in the screenshot above), double click on the _01_linear.R_ script. A new tab with that script opens up in the top-left section of RStudio's window. In that new window, select the following lines and press Ctrl+Enter. 

```script
constFun <- function(x) rep(3, length(x))
curve(constFun, -1, 6)
```

The combination of Ctrl+Enter actually executes a selected portion of a script, which causes multiple tabs to update:

* _Console_ (bottom-left section of the window) -- the executed code appears in this window (as well as possible errors and warnings)
* _Environment_ (top-right section of the window) -- the first line of the selected script defines a new object --namely a function called _constFun_. When this line has executed, the function will show up in the _Environment_ box.
* _Plots_ (bottom-right section of the window) -- the _Plots_ tab gets focus over the _Files_ tab and it contains a plot of a constant function _constFun_ when the second line of the script is executed.

![Files Tab]({{site.baseurl}}/images-hq/rstudio_execute.png)


# Further Learning Resources

## RStudio Wiki

* [Using RStudio](https://support.rstudio.com/hc/en-us/sections/200107586-Using-RStudio)

## YouTube

* [Getting started with R and RStudio](https://www.youtube.com/watch?v=lVKMsaWju8w)

{::comment}
# Opening and Saving Projects
# Workbench Overview
{:/comment}