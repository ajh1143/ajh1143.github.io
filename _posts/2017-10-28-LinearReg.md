---
layout: post
title: Linear Regression Analysis 
---

Let's talk about correlation.

General correlation is the quantification of a relationship between variables, most commonly represented as X & Y.
The goal of correlation is to identify a factor, X, that we can use to make useful predictions about Y. We'll get into the
philisophical arguments about extrapolation vs interpolation at another time, but for now, it's just something to mention. 

Ideally, we want to make causative connections between variables in data sets, but in the real world this is difficult due to the
wide array of interactions that truly exist. You often hear, "Correlation does not imply causation" thrown around. While this is 
true, it can be misleading. It does not imply causation, but it also doesn't negate it. In general, if you find high correlation,
you should continue whatever reasoning led you to that point, but refine your methods and ask further related questions.

Should you find correlation, you'll be presented with a number. That number will tell you a lot. It will tell you whether
the relationship is positive, with a upward sloping line, or a negative one, with a downward slope. It will tell you how strong 
the relationship is, a higher number implying a more useful predictive quality. Let's say you find a correlation of 0.75,
this simply means that 75% of your Y's behaviour can be predicted by variable X. We'd all like to be able to predict future
outcomes, and linear correlation is one way we can. It's not without risks if you dump resources into a faulty correlation, but 
when done correctly, the rewards can be worth it.

The most common method for linear regression is the Pearson method, a parametric test. 

Here's a bried overview

|Pearson Test|
|:------------:|
|Assumptions:|
|Linear associations|
|Continuous variables|
|Line Model - Y=mx+b|
|Data is normally distributed|
|Danger: Vulnerable to outliers|

There's always more theory to cover, and we will in the future. But for now, let's figure out how to run this powerful analysis
quickly, and pain-free with R. 
