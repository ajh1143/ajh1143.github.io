---
layout: post
title: "Fun with Web Scraping"
---

<img src="/Images/Scraping.jpg" class="block"/><br>
So, you want to grab data from a website, but there's no API to connect to?

What do you do? 

You get your hands dirty.

One solution is to utilize a scripting language to engage in manual data scraping.

In this case, we're going to probe the US Census website, and grab all the data we can.

Additionally, we want to make that data accessible as quickly as possible, so we're also going
to use the Pandas package to quickly transform the data into a dataframe, which will allow us to 
analyze the data immediately with Pandas, Numpy, or R. 

```python
   """
   AJH
   BeautifulSoup, Pandas, Python web scraper
   """

   from bs4 import BeautifulSoup
   from urllib.request import urlopen
   import pandas as pd
   import sys

   #Retrieves the user's desired text file 
   #output location in the form of C:\User\Name\Location
   def file_location():
       file_output_location = input("Enter a directory 
       for output of generated text files.")
       return file_output_location

   #Scraping method, iterates through each web page 
   #based on decade and creates a dict of the scraped 
   #data to be passed to df_print()
   def core_logic():
       output = file_location()
  
  for decade in range(1880, 2020, 10):
       page_decade = "https://www.ssa.gov/oact/
       babynames/decades/names"+str(decade)+"s.html"
       soup = BeautifulSoup(urlopen(page_decade))
       targets = soup.find_all("tr",{"align":"right"})
                                                  [1:]
                                                  
       data = {
           'Rank' : [],
           'Name_Male' : [],
           'Number_Male' : [],
           'Name_Female' : [],
           'Number_Female' : []
       }    
       
       for target in targets:
           target_acquired = target.get_text()
           z = target_acquired.split()
           data['Rank'].append(z[0])
           data['Name_Male'].append(z[1])
           data['Number_Male'].append(z[2])
           data['Name_Female'].append(z[3])
           data['Number_Female'].append(z[4])
       df_print(output, decade, data)

   #Transforms the dataset into a DataFrame using Pandas
   prints to the previously acquired output location        
   def df_print(file, year, populated_data_dict):
       file_output = file
       decade = year
       data = populated_data_dict
       pd.set_option('display.max_rows', 1000)
       df = pd.DataFrame(data)
       df = df[['Rank', 'Name_Male','Number_Male',
                   'Name_Female','Number_Female']]
       sys.stdout = open(file_output+"/"+str(decade)+
                                         ".txt", "w")
       print (df)
       sys.stdout.close()

   if __name__ == '__main__':
       core_logic()
```

Depending on your experience level, at first glance this can look intimidating, or like child's play. I'll assume you're relatively new to programming. 

## fileLocation()

In `fileLocation()` I'm simply asking the user to tell me which directory they'd like to output the scraped data to, this is just one way to approach the problem, it could easily be implemented with os.path as well. Once the program is initiated, the user's choice of output location will be where the complete set of text files will be stored.


## core_logic()
`core_logic()` is where the bulk of the action occurs. 

First, we implement `fileLocation()` and save the result of that into the variable 'output'. 

We now know where the files are going. But we need to understand what the data looks like to build the next feature. There is a separate page for each decade on census data, so we want to automate our method to scrape from each successive page//decade from 1880 to 2010. We do this with the standard `range(start, stop, increment)` design, and assign it to the variable 'decade'. We use 'decade' to alter the static portion of the web address, and insert our dynamic variable portion where needed to access each unique page in our algorithm. 

## BeautifulSoup
We're going to use BeautifulSoup, a package designed for precisely this use. This will connect us to each page we want, and we'll use `soup.find_all()` to extract our target portions of the source code of the website. This will be stored as 'targets'. We're going to use `.append()` to add the appropriate rows and columns to our dictionary data structure named 'data'. 

Remember the variable 'targets'? It's a set of rows of data, with what will become 5 columns, and we'll access row by row via another for loop, of each 'target' in 'targets'. But before we can store it, we need to clean it up before we place it in our 'data' dictionary. To do this, we'll use `.get_text()` and `.split()` to capture the core structures, the sex, a character string of the name, or the numeric string of the number of times recorded in the US census. We can then use index-based keys to place each column of semi-raw data, into our data structure.

## df_print()
After this process has been completed for a decade, we'll send the completed dictionary to `df_print()`, where we will use pandas to convert the dictionary into a formal data frame standard in R, via `Pandas.DataFrame()` to output a text file of each decade's content to our user-defined directory. 

