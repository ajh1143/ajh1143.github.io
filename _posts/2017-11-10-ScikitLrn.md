---
layout: post
title: Scikit-Learn Crash Course
---

<img src="/Images/scikit.jpg" class="inline"/><br>
Scikit-Learn is an essential tool for machine learning with Python

In this post, we're going to go through the fundamental features of Scikit-Learn. We will approach theory and real
world applications in another series. 

Until then, this will serve as a way to get familiar with the tools we can use.

# Loading Data
Before you begin writing any code, you need to understand where your data is coming from.

### Common Data Sources:
CSV
Text
Web

### Common Data Forms:
Pandas Dataframes
NumPy Arrays
SciPy Matrices

# Train and Test

`x_train, x_test, y_train, y_test = train_test_split(x, y, random_state=)`

# Pre-Processing

### 1. Standardize your data:

Scale -> transorm train -> transorm  test

`standardScaler().fit(x_train)`

`.transform(x_train)`

`.transorm(x_test)`

### 2. Normalize your data:

Normalize -> transform x_train -> transorm  test

`Normalizer().fit(x_train)`

`.transform(x_train)`

`.transform(x_test)`

### 3. Binarize your data:

`Binarizer(threshold= int).fit(x_data)`

`.transform(x_data)`

# Handling Missing Data

`Imputer(missing_values= int, strategy = 'mean', axis = int)`

`.fit_transform(x_data)`
