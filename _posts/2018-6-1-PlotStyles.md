---
layout: post
title: "MatPlotLib: Sampling Plot Styles"
---

<img src="/Images/Styles/style_title.jpg" class="inline"/><br>
Test your plot in every style. 


# Import MatPlotLib


```Python3 

import matplotlib.pyplot as plt

```

# Create a Class
```Python3

class PlotChoices():

```

# Methods

## Generate List of Possible Styles
```Python3  

    def PlotStyles(self):
    """
    Generate amd returns a list of the top 23 styles native to MatPlotLib
    """
        styles = plt.style.available
        return styles
        
```

## Generate Plots & Save Images To Folder

```Python3 

    def barPlots(self, dict_data, types):
    """
    Function: Uses dictionary dataset to create 23 different bar plots with different 
    styles selected
    Args:     dict_data: your datase, expected to be in dictionary format
              types: List of style names to use for each plot generated
          
    Note:     Define the dict_data parameter as 'default' to use a pre-set dataset
    """
        if dict_data == 'default':
            dict_data = {'Group A': 25, 'Group B': 50, 'Group C': 75}
        else:
            dict_data = dict_data
        names = list(dict_data.keys())
        values = list(dict_data.values())
        plt.figure(figsize=(8, 6))
        for each in types:
            plt.style.use(each)
            plt.bar(range(len(dict_data)), values, tick_label=names)
            plt.title('Style = ' + each)
            plt.xlabel('X-Axis Label')
            plt.ylabel('Y-Axis Label')
            plt.tight_layout()
            plt.savefig('PATH_TO_YOUR_OUTPUT_FOLDER'+each+'.png')
            plt.clf()

```

## Run It

``` Python3
if __name__ == "__main__"
    instance = PlotChoices()
    style = instance.PlotStyles()
    instance.barPlots('default', style)
```

# Our Results

## Classic
<img src="/Images/Styles/style_classic.png" class="inline"/><br>

## Classic_Test

<img src="/Images/Styles/style__classic_test.png" class="inline"/><br>

## BMH
<img src="/Images/Styles/style_bmh.png" class="inline"/><br>

## Dark Background
<img src="/Images/Styles/style_dark_background.png" class="inline"/><br>

## Seaborn Dark
<img src="/Images/Styles/style_seaborn-dark.png" class="inline"/><br>

## Seaborn Dark Palette
<img src="/Images/Styles/style_seaborn-dark-palette.png" class="inline"/><br>

## FiveThirtyEight
<img src="/Images/Styles/style_fivethirtyeight.png" class="inline"/><br>

## GGPlot
<img src="/Images/Styles/style_ggplot.png" class="inline"/><br>

## Seaborn Deep
<img src="/Images/Styles/style_seaborn-deep.png" class="inline"/><br>

## Seaborn Whitegrid
<img src="/Images/Styles/style_seaborn-whitegrid.png" class="inline"/><br>

## Seaborn Notebook
<img src="/Images/Styles/style_seaborn-notebook.png" class="inline"/><br>

## Greyscale
<img src="/Images/Styles/style_grayscale.png" class="inline"/><br>

## Seaborn Ticks
<img src="/Images/Styles/style_seaborn-ticks.png" class="inline"/><br>

## Seaborn Muted
<img src="/Images/Styles/style_seaborn-muted.png" class="inline"/><br>

## Seaborn Bright
<img src="/Images/Styles/style_seaborn-bright.png" class="inline"/><br>

## Seaborn Poster
<img src="/Images/Styles/style_seaborn-poster.png" class="inline"/><br>

## Seaborn White
<img src="/Images/Styles/style_seaborn-white.png" class="inline"/><br>

## Seaborn
<img src="/Images/Styles/style_seaborn.png" class="inline"/><br>

## Seaborn Talk
<img src="/Images/Styles/style_seaborn-talk.png" class="inline"/><br>

## Seaborn Darkgrid
<img src="/Images/Styles/style_seaborn-darkgrid.png" class="inline"/><br>

## Seaborn Paper
<img src="/Images/Styles/style_seaborn-paper.png" class="inline"/><br>

## Seaborn Colorblind
<img src="/Images/Styles/style_seaborn-colorblind.png" class="inline"/><br>

## Seaborn Pastel
<img src="/Images/Styles/style_seaborn-pastel.png" class="inline"/><br>
