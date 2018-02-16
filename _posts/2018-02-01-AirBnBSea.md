---
layout: post
title: Seattle AirBnB Analysis
---

<img src="/Images/airbnbsea.jpg" class="inline"/><br>
Where to rent, and where to avoid, if you'll be visiting Seattle. 

## Merging Multiple CSV Files into A Single File
```Python

import os
import pandas as pd
import matplotlib.pyplot as plt
plt.style.use('ggplot')
#IMPORT FILES
#SET DIRECTORY TARGET
dir = 'C:/Users/Andrew/Desktop/bitc1/s3_files/seattle/'
#SET FILES ALGORITHM
files = filter(lambda x: x.endswith('.csv'), os.listdir(dir))
#MERGE EACH FILE WITH CONCAT
for file in files:
    raw = pd.read_csv(dir+file)
    df = pd.DataFrame(raw)
    merged = pd.concat([df])
#SAVE OUTPUT FILE
merged.to_csv('C://Users//Andrew//Desktop//bitc1//s3_files//seattle//merged_final.csv')

```

## Viewing the merged file

```Python

#OPEN AND READ MERGED FILE
df = pd.read_csv('C://Users//Andrew//Desktop//bitc1//s3_files//seattle//merged_final.csv')

```
## Neighborhood Ratings

#### Extracting Relevant Columns

```Python

#EXTRACT SATISFACTION RATING AND NEIGHBORHOOD
df2 = df[['overall_satisfaction', 'neighborhood']]
#MAKE LIST OF NEIGHBORHOOD NAMES
names = df2['neighborhood'].unique()
#PIVOT DATAFRAME
df3 = df2.pivot(columns='neighborhood', values='overall_satisfaction')

```

#### Creating A New DataFrame

```Python

#CREATE NEW DF WITH HOOD, Sample, Average Rating
name_list = []
mean_list = []
count_list = []

for each in names:
    name_list.append(each)
    cur_mean = df3[each].mean()
    mean_list.append(cur_mean)
    cur_count = df3[each].count()
    count_list.append(cur_count)

raw_data = {    'Neighborhood' : name_list,
                'Sample_Size': count_list,
                'Average_Rating': mean_list}

df4 = pd.DataFrame(raw_data, columns = ['Neighborhood', 'Sample_Size', 'Average_Rating'])

```

#### Plotting The Top 5 Best, and Top 5 Worst Neighborhoods By Average Review 

```Python

sort_test = df4.sort_values('Average_Rating', ascending=[0])
x = sort_test.head(5)
x1 = sort_test.tail(5)
fig, axes = plt.subplots(nrows=1, ncols=2, figsize=(7, 8))
ax = x.plot.bar(color = "green", x= 'Neighborhood', y='Average_Rating', ax = axes[0], legend = False)
ax.set_ylim(top = 5)
ax.set_ylabel("Avg Rating (1-5)")
ax.set_xlabel("")
ax2 = x1.plot.bar(color = "orange", x= 'Neighborhood', y='Average_Rating', ax = axes[1], legend = False)
ax2.set_ylim(top = 5)
ax2.set_ylabel("")
ax2.set_xlabel("")
plt.tight_layout()
plt.show()

```
# Neighborhood Rankings

<img src="/Images/airbnbtop5.png" class="inline"/><br>

