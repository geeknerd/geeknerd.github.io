---
layout: post
title: Introduction to Machine Learning.
excerpt: ""
date: 2018-06-20
modifited: 2018-06-20
comments: true
pinned: true
tags: [Notes, Maching Learning]
image:
---

### Probability Theory
**Sum rule:** $$p(X)=\sum\limits_{Y} p(X,Y)$$  
**Product rule:** $$p(X,Y)=p(Y|X)p(X)$$  
**Symmetry property:** $$p(X,Y)=p(Y,X)$$  
**Normalization constant:** a constant to bring integral of a non-negative function to 1, e.g. to make it a probability density function.  
**Bayes' Rule:** $$p(Y|X)=\frac{p(X|Y)p(Y)}{p(X)}$$  
$$p(Y|X)$$: Posterior Probability. 
$$p(Y)$$: Prior Probability.  
$$p(X|Y)$$: Likelihood.  
$$p(X)$$: Evidence. Also the **normalization constant**: sum of the likelihood of X for each class Y.  
Building joint probability distributions depends on the number of variables $$N$$ as well as the number of states $$D$$, resulting a complexity of $$O(D^N)$$. Instead we could use fewer parameters by making **unconditional independence** assumptions (rare) or mediate the variable influences through 3rd random variable to achieve **conditional independence**.
