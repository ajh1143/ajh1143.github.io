---
layout: post
title: "Tipping Analysis"
---

<img src="/Images/Tips/tip_title.png" class="block"/><br>
Gratuity Optional?

# Import

```Python

import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

```

# Load Data

```Python

def getTipFile(fileName):
    raw_data = pd.read_csv(fileName)
    df = pd.DataFrame(raw_data)
    return df

```  
    
# EDA and Integrity

```Python

#Explore Data
def EDA(dataframe, outputpath):
    head = str(dataframe.head())
    desc = str(dataframe.describe())
    missing = str(dataframe.info())
    lineBreak = "---------------------------------------"
    text_data = (lineBreak, head, lineBreak, desc, lineBreak, missing, lineBreak)
    for each in text_data:
        print(each+'\n')
    print_EDA(outputpath, head, desc, dataframe, lineBreak)

#Print to File
def print_EDA(output, head, desc, df, lb):
    with open(output, "w") as file:
        file.write(lb+"\n")
        file.write(head+"\n"+lb +"\n")
        file.write(desc + "\n"+lb+"\n")
        f = open('dataframe.info()', 'w+')
        df.info(buf=file)
        f.close()
 
```

```Python

#Set Input and Output file name + locations
input_file = "tips.csv"
output_file = "tips_report.txt"

#Extract DataFrame
df1 = getTipFile(input_file)
#EDA
EDA(df1, output_file)

```

<img src="/Images/Tips/File_Tips.jpg" class="block"/><br>


# Pivot Table Plotting

### Sex and Tips

```Python

table = pd.pivot_table(df1, values='tip', index=['sex'], aggfunc= [np.mean, min, max])
table.plot(kind='bar', title = "Sex and Tips")
plt.xlabel("Sex \n (Male / Female)")
plt.ylabel("Customer Tips (USD)")
plt.grid(True)
plt.tight_layout()
plt.show()

```

<img src="/Images/Tips/S_Tips.png" class="block"/><br>


### Sex, Day of the Week, and Tips

```Python

table = pd.pivot_table(df1, values='tip', index=['sex', 'day'], aggfunc= [np.mean, min, max])
table.plot(kind='bar', title = "Sex and Day")
plt.xlabel("Sex and Day")
plt.ylabel("Customer Tips (USD)")
plt.grid(True)
plt.tight_layout()
plt.show()

```

<img src="/Images/Tips/SD_Tips.png" class="block"/><br>

### Sex, Smoker, and Tips

```Python

table = pd.pivot_table(df1, values='tip', index=['sex', 'smoker'], aggfunc= [np.mean, min, max])
table.plot(kind='bar', title = "Sex, Smokers, and Tips")
plt.xlabel("Sex and Smoker")
plt.ylabel("Customer Tips (USD)")
plt.grid(True)
plt.tight_layout()
plt.show()

```

<img src="/Images/Tips/SS_Tips.png" class="block"/><br>

### Sex, Day of the Week, Smoker and Tips

```Python

table = pd.pivot_table(df1, values='tip', index=['sex', 'day', 'smoker'], aggfunc= [np.mean, min, max])
table.plot(kind='bar', title = "Sex, Tips, Day, and Smokers")
plt.xlabel("Sex and Smoker Categories")
plt.ylabel("Customer Tips (USD)")
plt.grid(True)
plt.tight_layout()
plt.show()

```

<img src="/Images/Tips/STDS_Tips.png" class="block"/><br>

# Box Plot Comparison

### Sex, Day of the Week, and Tips

```Python

df1.boxplot(column='tip', by=['sex', 'smoker', 'day'])
plt.xticks(rotation=90)
plt.show()

```

<img src="/Images/Tips/Box_Tips.png" class="block"/><br>

# Binarize Data - The Easy Way

```Python

df1['sex'] = pd.Categorical(df1.sex).codes

```

<img src="/Images/Tips/Binarize_Tips.jpg" class="block"/><br>
