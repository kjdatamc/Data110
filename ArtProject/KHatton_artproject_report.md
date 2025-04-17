# Art Project Report
## Summary
Temperature blankets are knitting or crochet projects where different yarn colors are used to signify temperature ranges (called temperature gauges). I assigned colors to 10&deg; temperature gauges and applied them to Weather Underground data from the first quarter of 2025 for the Dulles Airport weather station. I chose to make a *temperature hat* with the stripes representing the weekly high and low temperatures and the pompoms representing the daily high and low temperatures.

![Image of Hat](https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png)

## Introduction

For my art project, I chose to adapt the *temperature blanket* concept, which is popular in knitting and crochet. A temperature blanket uses weather data to create a colorful representation of weather over a particular period. Often each row will represent a different day, and the row colors will represent the temperature of that day, with each color assigned to a particular temperature range (aka *temperature gauge*). There lots of varitions that can include other weather events, such as changing the stitch type depending on precipitation that day.

I chose to make a hat showing the high and low temperatures throughout the first quarter of 2025. I retrieved the historical data from [Weather Underground](https://www.wunderground.com/history/monthly/us/va/sterling/KIAD/date/2025-1), using the Dulles Airport weather station. The stripes of the hat represent the weekly highs and lows, and the pompoms represent all of the daily highs and lows.

## Exploratory Data Analysis (EDA)
I began my exploratory data analysis (EDA) by performing the `info` function to identify the columns in the dataset, then performing `describe` to understand the range of temperatures that I would be working with in order to set my temperature gauges.

### Setting Temperature Gauges
I had max and min temperature values ranging from 0&deg;F to 81&deg;F. *(Note that the 0&deg;F was a faulty data point)* I decided to use a simple range of 10&deg; for my temperature gauges, which perfectly matched the 9 colors of yarn I had available. Below is a sample of the code I used to set the temperature gauges that would be applied to two new columns for the max and min daily temperature.

```python
def label_max_gauge(row):
   if 0 <= row['Temp_Max'] < 10:
      return 0
   if 10 <= row['Temp_Max'] < 20:
      return 1
   if 20 <= row['Temp_Max'] < 30:
      return 2
   if 30 <= row['Temp_Max'] < 40:
      return 3
   if 40 <= row['Temp_Max'] < 50:
      return 4
   if 50 <= row['Temp_Max'] < 60:
      return 5
   if 60 <= row['Temp_Max'] < 70:
      return 6
   if 70 <= row['Temp_Max'] < 80:
      return 7
   if 80 <= row['Temp_Max'] < 90:
      return 8
   return
```

### Erroneous Data
I created a temperature gauge heatmap representing the weekly maximum temperature and the weekly minimum temperature. These colors would be used for the stripes of the body of the hat. When I first made the heatmap, I was surprised to see the coldest temperature gauge in the last week of the quarter. While a 0&deg;F low in week 4 seemed plausible, one in week 13 seemed unlikely. So, I graphed the daily temperatures and found the two 0&deg;F temperatures: Jan 22, 2025 and Mar 27, 2025.

<img
        src="https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png" 
        width=49%
        title="Image of Erroneous Temperature Gauge Heatmap"
        alt="Image of Erroneous Temperature Gauge Heatmap"
    />  &nbsp; <img
        src="https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png" 
        width=49%
        title="Image of Erroneous Daily Temperatures Line Graph"
        alt="Image of Erroneous Daily Temperatures Line Graph"
    />

Weather Underground offers the ability to view some weather data at the hourly level. When I did that for each of the days with 0&deg;F lows, I saw an apparent wind gust around the time that the temperature suddenly dropped to 0&deg;F. My interpretation is that a wind gust likely disabled the sensor and the 0&deg;F value should actually be a *null* value. On that assumption, I applied the lowest other recorded temperature for the days instead.

<img
        src="https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png" 
        width=49%
        title="Image of January 22 Hourly Temp and Wind"
        alt="Image of January 227 Hourly Temp and Wind"
    />  &nbsp; <img
        src="https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png" 
        width=49%
        title="Image of March 27 Hourly Temp and Wind"
        alt="Image of March 27 Hourly Temp and Wind"
    />

## Stripes
With the corrected dataset, I created a new temperature gauge heatmap representing the weekly maximum and minimum temperatures to identify the colors for the stripes of the body of the hat. Interestingly, there wasn't a single temperature gauge that appeared in both the weekly max and min temperatures.

![Image of Correct Temperature Gauge Heatmap](https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png)

## Pompoms

I created two bar graphs of the daily incidence of max and min temperatures in each temperature gauge. These would determine the proportion of colors used to make the pompoms. Unlike the weekly max/mins, the daily max and min temperatures have overlap of temperature gauges. The daily min temperatures have a more concentrated distribution compared to the max temperatures, which is to be expected based on the min temperature's lower standard deviation.

![Image of Temperature Gauge Bar Graph](https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png)

## The Hat
And here's the final hat!
![Image of Hat](https://github.com/kjdatamc/Data110/blob/d4cb729a97d8303a5969a4d46919aca5b25554a6/Project1/placeholder.png)
