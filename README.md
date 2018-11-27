# Bike Sharing in Boston

> Visualization techniques: **Calendar Heat map**, **Polar Chart**, **Radar Plot**, and **Overlapped bean plots**

## Introduction 
The data used for this project is about bike sharing in Boston (2011-2012). The main objective of this analysis is to explore the reasons and elements that affect the number of bike rentals. Four different visualization techniques including calendar heat map, polar chart, radar plot, and overlapped bean plots are used to explore different aspects of data and display some interesting patterns

## Data Overview
There are two datasets in the format of CSV files gained from *UCL Machine Learning Repository*. You can find this dataset [here](https://archive.ics.uci.edu/ml/datasets/bike+sharing+dataset).
1. *Day.csv*
The numbers of bike rentals are recorded on daily basis. There are 731 records and 16 variables.
2. *Hour.csv*
The numbers of bike rentals were recorded on hourly basis. There are 17,379 records and 17 variables. The variables in bold are the ones used in our analysis from different aspects. 

## Methodology
### Calendar Heat map
* Motivation<br/>
The calendar heat map is applied to display the total rental counts from the date aspect of the dataset. It can visualize the value in week, month, and year which is an organized way most people get used to. It also makes the comparison easier since audiences only need to notice the change of color. What’s more, it can convey the pattern from a seasonal aspect. Compared with other techniques like bar graph and scatter plot, the calendar heat map can display more information in an organized way.

* Data manipulation<br/>
date and rental counts are used as a date aspect for Calendar Heat map. Some data manipulation works have been done to plot this heat map. New columns named day, month, year are extracted by using strftime function with %e, %b, %Y, respectively, from the original column named date. The draft of heat map could only plot one-year data at a time and the days of each month were vertically stacked into one column while months were displayed horizontally. Data should be divided into two years and then plotted individually in the draft of the heat map. It made comparison hard because it did not follow up the habits of people when the check the date. The Calendar heat map solves this problem. The data manipulation works including change the format of the date, normalize values of casual and registered, and subset the casual and registered users for each year to gain four datasets. 

* Visualization<br/>

The bolded title is about the topic of bike sharing in Boston. X-axis stands for the month, Y axis stands for the day of the week, and each cell stands for a day. The colors can convey the number of rental counts(normalized) with legend. 

The calendar heat map makes comparison easier compared with normal heat map. Because it adjusted the layout of week and month corresponding to real calendar making people easier to read the graph. 
A function to design calendar heat map is provided by Dr.Paul Bleicher. Parts of codes are revised to change the displayed color. The original color is designed stating from green to red. The transition part of color may make people confused that cells marked in white of calendar heat map have lower rent count than some cells are marked in green have. Actually, the cells marked in white have higher value than cells marked in green because the color range starts from green and then changes to while and approach to red finally. The color range is reset to five scale staring from white, light yellow, light green, light blue, and dark blue. It matches with people’s visualized intuition and avoids confusion of transition color.  The colors are selected by using Color Brewer and tested for multiple times. The final five colors are #F1EEF6","#FFFFCC","#A1DAB4","#2C7FB8","#253494". The size of tick marks on Y is enlarged to make the day of week can easily for audiences. The legend with colors and corresponding values can facilitate audiences see rough values in cells of calendar heat map.

