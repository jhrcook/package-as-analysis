--- 
title: "Package as Analysis"
author: "Joshua H. Cook"
url: 'https\://jhrcook.github.io/package-as-analysis/.'
github-repo: jhrcook/package-as-analysis
twitter-handle: JoshDoesa
cover-image: cover.png
date: "2019-03-10"
site: bookdown::bookdown_site
documentclass: book
bibliography: book.bib
biblio-style: apalike
link-citations: yes
description: "This is a manual for how to conduct data science analysis using the standard R package framework."
---

# Welcome {-} <img src="cover.png" width="250" height="366" align="right" alt="Cover image" />

This is a manual on how to use the standard R package framework for data analysis. Though potentially more work, especially at the start, the purpose of using the R package framework is to maintain a clear and reproducible analysis. 

## Advantages

There are many advantages to using this framework. Here are just a few, though I am sure you will find there are many others:

* Because this is a standard framework, other will be able to navigate the directories and files adeptly.
* The implementation of tests on functions and subroutines will make bugs easier to find and increase overall confidence in the validity of the analysis
* This is a seamless mixture of scripts and markdown files for the separation of functions and analysis
* Complete documentation of functions makes returning to code later much easier!
* The analysis can take advantage of normal R package tools such as [Travis-CL](https://travis-ci.org) and [Codecov](https://codecov.io) integration, [pkgdown](https://pkgdown.r-lib.org), and [devtools](https://devtools.r-lib.org) (build checks, documentation, etc.).

