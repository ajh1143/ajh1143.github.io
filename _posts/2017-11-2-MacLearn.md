---
layout: post
title: Machine Learning 101 - Part 1
---

It's hot, it's trendy, it's powerful. Let's dive in together using Python. 

So, you have a set of data you want to explore. In our case, we're going to use an example dataset from the UCI Machine Learning
Repository. In particular, we're going to explore Abalone data from: 

`Warwick J Nash, Tracy L Sellers, Simon R Talbot, Andrew J Cawthorn and Wes B Ford (1994)`
`The Population Biology of Abalone (_Haliotis_ species) in Tasmania. I. Blacklip Abalone (_H. rubra_) from the North Coast and   
Islands of Bass Strait`
`Sea Fisheries Division, Technical Report No. 48 (ISSN 1034-3288)`

## What You See Is What You Get

The first thing you want to do, is find out what your dataset actually looks like.

We need to import the Pandas package for Python, which we'll import as pd:

`import Pandas as pd`

Then we need to connect to the data structure, by calling: 

`pd.read_csv(data_url, names = columns)`

`data_url = "https://archive.ics.uci.edu/ml/machine-learning-databases/abalone/abalone.data"`

We can look at the dataset directly, and find out the order and column names, which we'll set as /"columns/":

`columns = ['Sex','Length','Diameter','Height','WholeWeight', 'ShuckedWeight', 'VisceraWeight', 'ShellWeight', 'Rings']`

Now, we can connect to our data with the proper parameters.

`data = pd.read_csv(data_url, names=columns)`

Done!

Next, we should explore the data more intimately. First, let's find out how many rows and columns we're actually dealing with.

## Find Rows and Columns
We can view the total number of Rows and Columns by using `data.shape`:

`print(data.shape)`

|output|
|:----:|
|(4177, 9)|

4000+ rows over 9 categories! 

## View Your Data
We can see what a sample of our dataset looks like by using `data.head(#of rows)`:

`print(data.head(3))`

```  
Sex  Length  Diameter  Height  WholeWeight  ShuckedWeight  VisceraWeight  \
0   M   0.455     0.365   0.095       0.5140         0.2245         0.1010   
1   M   0.350     0.265   0.090       0.2255         0.0995         0.0485   
2   F   0.530     0.420   0.135       0.6770         0.2565         0.1415   

   ShellWeight  Rings  
0         0.15     15  
1         0.07      7  
2         0.21      9  
```


## Assay Missing Values
We should also check for missing values, too many can cause problems, but we can massage the data by applying an average in place of NA values, if the number missing is low enough, without introducing an extreme error rate

`print(data.isnull().sum())`

|Category|Missing Values|
|:--:|:--:|
|Sex  |  0|
|Length    |       0|
|Diameter   |      0|
|Height      |     0|
|WholeWeight  |    0|
|ShuckedWeight |   0|
|VisceraWeight  |  0|
|ShellWeight     | 0|
|Rings            |0|
|dtype: |int64|

No values are missing, this is ideal!


## Set Bins
We can also bin our categories by Sex(or any other column if it is a categorical type) and see a count for each: 

`print(data.groupby('Sex').size())`

|Sex|Count|
|:--:|:--:|
|F   | 1307|
|I   | 1342|
|M    |1528|
|dtype:| int64|
