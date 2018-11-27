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
<img width="1370" alt="screen shot 2018-11-27 at 3 13 48 pm" src="https://user-images.githubusercontent.com/31257555/49111970-2f091100-f257-11e8-8e9a-7ccfb8b2e1da.png"><br/>
<img width="1341" alt="screen shot 2018-11-27 at 3 13 59 pm" src="https://user-images.githubusercontent.com/31257555/49111972-316b6b00-f257-11e8-9826-83e3374ccc34.png"><br/>
<img width="1343" alt="screen shot 2018-11-27 at 3 14 09 pm" src="https://user-images.githubusercontent.com/31257555/49111974-33352e80-f257-11e8-9169-0fcc2be440e3.png"><br/>
<img width="1364" alt="screen shot 2018-11-27 at 3 14 17 pm" src="https://user-images.githubusercontent.com/31257555/49111981-35978880-f257-11e8-9cbd-a0d6bb0d0fbe.png"><br/>
The bolded title is about the topic of bike sharing in Boston. X-axis stands for the month, Y axis stands for the day of the week, and each cell stands for a day. The colors can convey the number of rental counts(normalized) with legend.<br/>
The calendar heat map makes comparison easier compared with normal heat map. Because it adjusted the layout of week and month corresponding to real calendar making people easier to read the graph.A function to design calendar heat map is provided by Dr.Paul Bleicher. Parts of codes are revised to change the displayed color. The original color is designed stating from green to red. The transition part of color may make people confused that cells marked in white of calendar heat map have lower rent count than some cells are marked in green have. Actually, the cells marked in white have higher value than cells marked in green because the color range starts from green and then changes to while and approach to red finally. The color range is reset to five scale staring from white, light yellow, light green, light blue, and dark blue. It matches with people’s visualized intuition and avoids confusion of transition color.  The colors are selected by using Color Brewer and tested for multiple times. The final five colors are #F1EEF6","#FFFFCC","#A1DAB4","#2C7FB8","#253494". The size of tick marks on Y is enlarged to make the day of week can easily for audiences. The legend with colors and corresponding values can facilitate audiences see rough values in cells of calendar heat map.

* Results and Findings 
  * The total rental counts in 2012 is larger than that in 2011.
  * Users tend to rent bikes most during the period from April to Oct in both years. The weather in these months could have affected users’ behaviors which will be discussed in the next graph. 
  * Casual users are more like to rent bikes during weekends while registered users are more like to rent bike during weekdays.

### Polar charts
* Motivation<br/>
When we mentioned the time, the intuition of time will be a clock. This is the reason to use the polar chart to explore the data from time aspects. The polar chart shows the different time of a day which makes people easier to see the pattern of different types of users. The 24 hours are plotted into a circle. Compared with bar chart, the polar charts can visually give the general idea about time of information we want to convey. Two types of users are plotted on same baseline which will not distort the data. As you can see, the small circle in the middle is the baseline for two types of users. Looking inside of the small circle, you can see the values of casual users in 24 hours and find what time will have more or fewer casual users rent the sharing bikes. Looking outside of the small circle, you can see the values of registered users. What’s more, there is another comparison can be made by looking at the same time for two types of users.  
 
* Data manipulation <br/>
Hour, casual, registered, and rental counts are used as time aspect for polar chart. Many data manipulation works have done for preparing for using polar chart. New columns named day, month, and year are extract by using strftime function with %e, %b, %Y, respectively, from original columns named date. To avoid data distortion, the values of casual and registered are recalculated by using square root shown in Figure.1. (bike$registered = sqrt(bike$registered), bike$casual= sqrt(bike$casual). In order to show the difference, the graph plotted by bike$registered with bike$casual is also displayed as below Figure.2. The data is melted keeping all variables in original datasets except for casual and registered users. The method is used to melt data by using melt(bike,c("instant","dteday","season",….) and then casual and registered are combined to one column, generating a new column named Value which is corresponding to the column named Variable. The new dataset named melt_hour is generated, and it is aggregated based on hr (hour) and Variable gaining the hourly mean of rental counts by using aggregate (value~ hr+ variable, melt_hour, mean). The mean is used instead of sum because the mean makes more sense for measuring people’s behavior.

* Visualization <br/>
Figure 1. (Good) <br/>  
Figure 2. (Distortion)<br/>
The bolded title is about the topic of Rental Count vs Hour for different User Type. X-axis stands for time of day which is changed to be a circle, Y axis stands for the average rental counts. The green color stands for casual users and orange stands for registered users by looking at the legend on the right of graph.The geom_bar() and coord_polar(position = "stack") are used to generate polar chart. The data used is aggregated by hour. X-axis is hr(hour), the Y-axis is the variable named new which created by changing the value of average rent count to be negative if the users are casual users. The effect you can see this adjustment is the casual users marked in green are inside of the small circle, while the registered users marked in orange are outside of the small circle. The colors are selected by using Color Brewer and tested for multiple time to achieve the best display. The green means that casual users are potential registered uses conveying the prospect meaning. The orange color is a good matched with green and make comparison easier. The colors of bars are set by using scale_fill_manual(values=c("#66c2a4","#fdbb84")). The label of X is relabeled by using time instead of number.

* Results and Findings
  * Registered users rent bikes the most around 8:00 am and from 4:00 to 6:00 pm. However, casual users rent bikes the most from 10:00 am to 7:00 pm. This can be explained that registered users rent bikes to commute while casuals rent bikes only to move around casually or occasionally.
  * The rental counts of registered users are larger than that of casual users.


### Radar plot
* Motivation<br/>
Weather was a really interesting and challenging aspect to visualize and what was more challenging that weather can affect rentals in terms of many different variables such as temperature, humidity, wind speed, and weather type (clear, mist, rainy or snowy). Radar charts can definitely do the job since many attributes can be easily compared at the same time. Three different radar graphs were plotted in one graph. Each graph can compare how users behave in different weather types in terms of each weather aspect. The first graph shows how the temperature affects rental counts in three different cases of weather types. These different weather types were represented by 3 different colors in each graph. The second graph follow the same pattern and presents how humidity impacts the rentals for each weather type. The last radar plot expresses how wind speed affects the user behavior for the 3 different weather types. Furthermore, we can compare how different these weather aspects affect rentals by comparing the different radar plots at a time.

* Data manipulation<br/>
The data was collected as numerical records for all the variables from the daily basis dataset. In order to plot a radar graph, data should be divided into intervals or levels and then plot the average rental counts of each level. International standards were used to create intervals for temperature, wind speed, and humidity. All aspects were divided into 5 ranges of records so that we can keep our radar plots consistent.  The start of each graph is similar to starting a bar graph for 3 different variables with a different color for each. The axis of each interval in each radar plot represents the rental counts and shares the same tick marks and scale. Data manipulation was required to get appropriate radar plots. 
In the temperature aspect, all records had to be multiplied by 41 to be converted from normalized to Celsius, then it was converted from Celsius to Fahrenheit. After checking the minimum and maximum temperature in Fahrenheit, records were divided in ranges as follow :[76-105) for hot, [68-76) for warm, [59-68) for mild, [45-59) for cold, and [32-45) for very cold.
In the wind speed aspect, records had to be multiplied by 67, then converted into levels of ranges in km/hr. [1-5) for light air, [5-12) for light breeze, [12-19) for gentle breeze, [19-28) for moderate breeze, and [28-39) for fresh breeze. In the humidity aspect, records had to be multiplied by 100, then converted into 5 equal levels of percentages from 0 to 100%.
For each radar plot, a new dataset is created from the original one where all unwanted columns were removed. For the temperature radar graph, weather type, temperature type, and rental counts columns were the only ones kept. For the wind speed radar graph, the only kept columns were weather type, wind speed type, and rental counts. For the humidity radar graph, weather type, humidity range, and rental counts were the only columns kept. 
A summarized data set of each one was created by calculating the average rentals for each different pair of the aspect and the weather type using the ddply function. To implement the code for these radar plots, we had to change the shape of how these data sets looked like after all. cast( ) function was used so that the main aspect column’s records can become columns. For example, in the temperature aspect dataset, columns become (hot, warm, mild, cold, very cold, and weather type) and the average rentals become our records. Then, is.na( ) function was used to replace all the non-available records by 0. The weather type column with (1, 2, 3) records was removed and replaced to be recognized by the rows’ names. These rows’ names were changed to ("Clear or Cloudy", "Mist", "Light Rain or Snow"). Then, two records were added as the first and second record to the three datasets of the three aspects. The first row is the largest number of average rentals within all aspects only 5952.348 for all intervals and the second row is all zeros. Now, we have 5 columns (intervals) and 5 rows (records) for each weather aspect. 

* Visualization<br/>
The techniques were used in this graph combine three different weather types with three different weather aspects. Radar plot and colors together create a rich and deep display of how weather affected rentals by looking at different weather variables at a time. Also, radar plots are easy to put together in one graph because of their shape and round plot. 
The colors were chosen by using the web so colors can give a clear visualization when they overlap. For borders, rgb(0.2,0.5,0.5,0.9), rgb(0.8,0.2,0.5,0.9) , and rgb(0.7,0.5,0.1,0.9) were used. For fill in colors, rgb(0.2,0.5,0.5,0.4), rgb(0.8,0.2,0.5,0.4), rgb(0.7,0.5,0.1,0.4) were used. 
The organization of each radar plot intervals was based on the numerical order of each plot except for the temperature graph. In temperature, regular order was used but then we realized that it’s better to emphasize the difference between hot, cold, and very cold temperature so the steep difference can be more obvious to audience by changing the order of temperature levels. I used photoshop to combine the radar plots in one graph and adjusted all of them to have the same size. The scale we used was based on minimum and maximum rentals of all aspects. 
 
* Results and Findings<br/>
  * When the weather is clear, users rent bikes the most especially when the temperature is hot or warm.
  * When humidity is 40 % or above and the weather is clear, users tend to rent more bikes.
  * Winds have had an impact on users’ behavior and users have rented most when there is light breeze. Fresh breeze makes people rent bikes only when the weather is clear and not when it’s mist or rainy. In contrary, light air makes users rent bikes only when it’s not rainy. 
  * In general, light rain and snow impacted rentals negatively and users don’t rent bikes in such weather.
  * Users rent the most when it’s warm but the colder the weather is, the less rentals we have.

### Overlapped Bean plots or Two Split-Violin plots
* Motivation<br/>
Bike rentals in different seasons can have different behavioral changes especially with the fact that each season can be different from one place to another and could have changeable weather as well. Studying rental behavior changes in terms of seasonal changes for different years in one graph was a bit of a challenge. What was more challenging as we were enhancing our graph is to add another aspect to the visualization comparison which is the user-type aspect. Violin graphs can plot the distribution of rentals for each season. Bean plots or violin split graphs can split these violins to show the rental distributions for each season in two different years. We wanted to try a new technique to add a different aspect to this graph and see if it works since we had the idea of it. To add a new aspect, overlaying bean plots was our final thought to show all these distributions in one graph. It was a bit of challenge to plot 16 different violins in one graph which have to be managed around 4 seasonal lines.

* Data manipulation <br/>
In this graph, we used the daily basis dataset. A new dataset was created by removing all unwanted columns and melting different user types in one column. Also, seasons have been changed from numerical values to season names so do the years values. Our new dataset will have year, season, user type, and rental counts columns. The Y axis will represent the rental counts and X axis will represent different seasons. Each season will have two overlapped bean plots. The first bean plot is for casual users’ rentals in 2011 and 2012. The second overlapped bean plot is for registered users’ rentals in 2011 and 2012. geom_split_violin function was used to split these violins. Furthermore, color in aesthetics of ggplot was used to distinguish between different years. On the other hand, fill in aesthetics of ggplot was used to distinguish between different user types.

* Visualization<br/>
The techniques used in this graph combine 4 different aspects to be in one graph. This shows a deep and rich display of the data so the comparison can be wider and variate. It gives a clear visualization on how the distribution of rental behavior has changes over different seasons as well as over different years for different user types. Colors were chosen after many attempts of many different choices since every color has to reflect with the other three colors. For borders, 3182bd and rgb(0.8,0.2,0.5,0.9) were used. For fill in colors, #fff7bc and rgb(0.2,0.5,0.5,0.9) were used. Also, we tried to use different scales such as logarithmic scale but they distorted the data. The problem we encountered is how to plot the mean of each curve in the appropriate place of x value since we have 16 means, which we managed at the end by adjusting the size of the mean line and its position until we determined the most adequate visualization. 

* Results and Findings
  * Users tend to use bikes in Fall more than they do in any other seasons in both years.
  * Users tend to rent bikes the least in Spring in both years.
  * Registered users rent bikes more than casual users in all seasons in both years.
  * Fall, Winter, and Summer have similar distributions with slight differences in both years. Spring distribution was different and daily rentals for casual users were clustered around small values (0-300).
  * Rental counts have increased in the second year in all seasons and for all users.


## Conclusion 
In conclusion, these graphs have told us so much about how rentals were driven in these two years and what variables affected users’ behaviors the most.
* The rental counts have increased in the second year which could be due to the increasing number of registered users as well as casual users.
* Users tend to rent bike the most when the weather is clear and the temperature is warm or hot.
* The registered users rent bikes more often which could be due to their reliability to go to work, school and other usual places. While casual users only use them occasionally.
*	Users do not normally rent bikes when the weather is rainy or very cold.
* Spring had the least number of rentals among all other seasons in both years.
* Rental counts were the most around rush hours and the least at night which could be due to the nature of most people jobs and school time.

## Future Work
*	To identify days that are neither holiday nor weekends and have high rental counts (Calendar heat map).
*	To see if customers’ usage behavior is the same or different in 2011 and 2012 (Polar chart).
* To see if different user types behave differently in weekends and holidays.
* To see how working days can affect rentals in terms of weather changes especially for registered users.

