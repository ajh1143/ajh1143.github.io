---
layout: post
title: Seattle AirBnB Analysis
---

<img src="/Images/airbnbsea.jpg" class="inline"/><br>
Where to rent, and where to avoid, if you'll be visiting Seattle. 

We'll begin diving into our analysis by obtaining relevant datasets. We'll use the public information located here: `https://s3.amazonaws.com/tomslee-airbnb-data-2/seattle.zip` This zip file contains 22 csv files containing data recorded
by AirBnB about the Seattle area market from September 2015 through July 2017 in monthly intervals. 

Rather than dealing with each month as a separate entity, we're going to merge all 22 files into a single csv file, using
Pandas concatenation, lambda filtering, and the OS package. The code below will walk you through the steps to complete this task.

## Merging Multiple CSV Files into A Single File

```Python

import os
import pandas as pd
import matplotlib.pyplot as plt

#IMPORT FILES
#SET DIRECTORY TARGET
dir = 'C:/Users/Andrew/Desktop/seattle/'
#SET FILES ALGORITHM
files = filter(lambda x: x.endswith('.csv'), os.listdir(dir))

#MERGE EACH FILE WITH CONCAT
for file in files:
    raw = pd.read_csv(dir+file)
    df = pd.DataFrame(raw)
    merged = pd.concat([df])

#SAVE OUTPUT FILE
merged.to_csv('C://Users//Andrew//Desktop//seattle//merged_final.csv')

```

Great! We've compiled all of our data into a single (but long) file and preserved the original csv structure.

I manually looked at the file and noticed two columns I was personally interested in, `Neightborhood` and `Overall_Satisfaction`. The neighborhood is where the AirBnB rental is located in the city, and the Overall_Satisfaction is a 
user rating of their satisfaction with the rental.

The workflow we're going to pursue will be to extract these two columns, and create a new DataFrame for analysis

#### Viewing the merged file

```Python

#OPEN AND READ MERGED FILE
df = pd.read_csv('C://Users//Andrew//Desktop//seattle//merged_final.csv')

```
# Neighborhood Ratings

According to our plan, let's extract the two target columns and associated observations and save them as a new dataframe called df2. We'll also want to gather a list of neighborhoods using the `.unique()` command, which will return us a list of all unique
neighborhood names recorded in the AirBnB dataset. 

We'll then pivot our new DataFrame so that the unique neighborhoods are displayed as columnar categories and rows populated by the users' reported satisfaction ratings, and save this as df3.

#### Extracting Relevant Columns

```Python

#EXTRACT SATISFACTION RATING AND NEIGHBORHOOD
df2 = df[['overall_satisfaction', 'neighborhood']]

#MAKE LIST OF NEIGHBORHOOD NAMES
names = df2['neighborhood'].unique()

#PIVOT DATAFRAME
df3 = df2.pivot(columns='neighborhood', values='overall_satisfaction')

```

Cool! Let's continue.

We're going to create another Pandas DataFrame, but this time we're going to manually create it using our previous data and light analysis. 

This new DataFrame will consist of 3 columns, `Neightborhood`, `Sample_Size`, and `Average_Rating`. As you can see, `Sample_Size` is new, and we're going to create it by counting the number of recorded ratings left by users of the service so we can assay an informal level of trust in the ratings. Obviously a very high or low rating would be suspicious if we're dealing with a handful or fewer reviews, it might be disgruntled customers or AirBnB hosts leaving themselves positive scores. Personally, I think a minimum of 50 reviews would be a good cutoff for a neighborhood, but we'll deal with that later. 

We're also going to generate an Average rating for each neighborhood, by using `.mean()` on each neighborhood column and returning the score. 

We'll continue by appending each category to a separate list, and then compiling the lists into a Dict data structure that we will then use to generate the actual DataFrame. 

Follow along below!

#### Creating A New DataFrame

```Python

#Create new dataframe with N.Hood, Sample, Average Rating
name_list = []
mean_list = []
count_list = []

#Add Targets to Lists
for each in names:
    name_list.append(each)
    cur_mean = df3[each].mean()
    mean_list.append(cur_mean)
    cur_count = df3[each].count()
    count_list.append(cur_count)

#Create Dict from Lists
raw_data = {'Neighborhood' : name_list,
            'Sample_Size': count_list,
            'Average_Rating': mean_list}

#Create DataFrame from Dict, Specify Columns
df4 = pd.DataFrame(raw_data, columns = ['Neighborhood', 'Sample_Size', 'Average_Rating'])

```

Great! Now, how does our distribution look? I don't want to deal with a messy graph, and neither do you. So let's constrain
our results to the Top 5 Best, and Top 5 Worst neighborhoods to rent an AirBnB, by average review.

#### Plotting The Top 5 Best, and Top 5 Worst Neighborhoods By Average Review 

```Python

#Sort New DataFrame in Ascending Order
sort_test = df4.sort_values('Average_Rating', ascending=[0])

#Extract Top 5 and Bottom 5 Elements of Sorted DataFrame 
x = sort_test.head(5)
x1 = sort_test.tail(5)

#Set Plot Style
plt.style.use('ggplot')

#Structure Plot, 1 Row and 2 Columns (Creates Side By Side Plot)
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(7, 8))

#Build Plot

#Figure 1 (Top 5 Best Rated Neighborhoods)
ax = x.plot.bar(color = "green", x= 'Neighborhood', y='Average_Rating', ax = axes[0], legend = False)
ax.set_ylim(top = 5)
ax.set_ylabel("Avg Rating (1-5)")
ax.set_xlabel("")

#Figure 2 (Bottom 5 Worst Rated Neighborhoods)
ax2 = x1.plot.bar(color = "orange", x= 'Neighborhood', y='Average_Rating', ax = axes[1], legend = False)
ax2.set_ylim(top = 5)
ax2.set_ylabel("")
ax2.set_xlabel("")

#Fit Plot and Show Plot
plt.tight_layout()
plt.show()

```
## Neighborhood Results

<img src="/Images/airbnbtop5.png" class="inline"/><br>

