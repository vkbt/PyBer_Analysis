# Visualization and analysis of rideshare data for PyBer

## Overview

We have been asked to analyze and add visualization of all the rideshare data from January to April 2019 for V. Isualize, the CEO of PyBer, a ride-sharing app company. The result of our analysis and visualizations will help PyBer improve access to ridesharing services and determine affordability for underserved neighborhoods.

## Resources
 - Data Source: [**city_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/city_data.csv), [**ride_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/ride_data.csv)
 - Software: Anaconda **2022.05**, Python **3.7.13**, Conda **22.9.0**, Jupyter Notebook **6.4.12**, Pandas **1.3.5**, Matplotlib **3.5.2**
 
## Summary
We used three phase process (collect, prepare and analyze) to analyze the data and added a multiple line chart where each week is a peak or dip in the line graphs to make the analysis visually more compelling and informative.

### 1. Collect the data

We received 2 csv files with raw data to perform analysis for PyBer: [**city_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/city_data.csv), [**ride_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/ride_data.csv).

Using **Conda** package management system we created a new virtual environment that runs the latest version of **Python 3.7** and contains all the **Anaconda** packages including **Jupyter Notebook** and named it PythonData. **Jupyter Notebook** is a powerful interactive computional environment that supports **Python** and is largely used for data analysis and visualization. We imported the data into Jupyter Notebook using [**os**](https://docs.python.org/3/library/os.html) module and read the data using [**pandas.read_csv**](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) function.  We used **Pandas**, a fast and powerful software library built on top of **Python**, to clean, manipulate and analyze the data. We also used **Matplotlib** to help us visualise the data. [**Matplotlib**](https://matplotlib.org) is a comprehensive library for creating static, animated, and interactive visualizations in Python.

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/1_new_pandas_os_import.png" width=100% height=100%>

### 2. Prepare the data

It is essential to clean the data before we analyze it. We used built-in Pandas functions below to handle missing data, duplicated data and incorrect data types:
- [**pandas.DataFrame.isna**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.isna.html) function to identify missing values and [**pandas.DataFrame.dropna**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html) function to remove rows with missing values
- [**pandas.DataFrame.duplicated**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html) function to identify duplicate values and [**pandas.DataFrame.drop_duplicates**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html) function to remove duplicates

We merged [**city_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/city_data.csv) and [**ride_data.csv**](https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/ride_data.csv) using [**pandas.DataFrame.merge**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.merge.html?highlight=merge#) function and moved to the analysis step.

### 3. Analyze the data

We started with high level data analysis and created 5 separate [data series](https://pandas.pydata.org/docs/reference/series.html):

- total rides count by city type (Urban, Suburban and Rural) using [**.pandas.DataFrame.groupby**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) and [**pandas.DataFrame.count**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.count.html) function

- total drivers count by city type using [**.pandas.DataFrame.groupby**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) and [**pandas.DataFrame.sum**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sum.html) function

- total of all fares by city type using [**.pandas.DataFrame.groupby**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html) and [**pandas.DataFrame.sum**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sum.html) function

- mean fare amount per ride by city type by dividing previously calculated total of all fares by total rides
- mean fare amount per driver by city type by dividing previously calculated total of all fares by total drivers

Using these 5 data series we created a new summary data frame and formatted it using [**pandas.DataFrame.style.format**](https://pandas.pydata.org/docs/reference/api/pandas.io.formats.style.Styler.format.html) function.
<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/3_new_create_a_new_data_frame_from_series.png" width=100% height=100%>
<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/4_new_format_a_data_frame.png" width=100% height=100%>

We started with adding **%matplotlib inline** [magic command](https://ipython.readthedocs.io/en/stable/interactive/magics.html). This command provides support for Matplotlib to display figures and graphs directly inline in the Jupyter Notebook.

 Using [**pandas.DataFrame.groupby**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html), [**pandas.DataFrame.reset_index**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html) and [**pandas.DataFrame.pivot**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.pivot.html) functions we reshaped the data to have the date as index, city type as columns and fare as values.

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/7_new_pandas_pivot_function.png" width=100% height=100%>
 
We converted the dates to pandas datetime object format using [**pandas.to_datetime**](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html) function. Using [**pandas.DataFrame.loc**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html) function we filtered the data from January to April and using [**pandas.DataFrame.resample**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.resample.html) function we organized the data into weekly bins.

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/8_new_pandas_to_datetime_function.png" width=100% height=100%>

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/9_new_pandas_loc_function.png" width=100% height=100%>

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/10_new_pandas_resample_function.png" width=100% height=100%>

#### Visualizing the data:

Finally we created a multiple line chart showing the total fares using [**pandas.DataFrame.plot**](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.plot.html) function.  We applied ["fivethirtyeight"](https://matplotlib.org/stable/gallery/style_sheets/fivethirtyeight.html) style, annotated the chart and saved it as png image file.


<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/11_new_pandas_mutiple_line_chart.png" width=100% height=100%>

## Multiple line chart of total fares by city type from January to April 2019

<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Analysis/PyBer_fare_summary.png" width=100% height=100%>

## Conclusion

Working on the Pyber data we grouped results by urban, rural and suburban city types using our **Python**,  **Pandas**, **Jupyter Notebook** and **Matplotlib** skills. 


<img src="https://github.com/vkbt/PyBer_Analysis/blob/main/Resources/12_new_final_data_frame_for_summary.png" width=100% height=100%>

According to our analysis the total number of drivers is 2,405, 490 and 78 in urban, suburban and rural areas respectively. We can see that even though there are less drivers in rural areas, these drivers get almost 3x the rides per driver comparing to urban drivers and 2x comparing to suburban drivers. By analizing average fare per ride and average fare per driver we can see the law of supply and demand. The average fare per driver($16.57) and per ride is lower in the urban areas where the amount of drivers(2,405) and the amount of rides(1,625) is the highest. Similarly, the fare per ride and per driver is the highest in the rural areas where there is less drivers. Urban drivers receive $24.53 per ride and $16.57 per driver, suburban drivers receive $30.97 per drive and $39.50 per driver, rural drivers receive $34.62 per ride and $55.49 per driver. Total fares for urban cities was $39,854.38, suburban was $19,356.33 and rural was $4,327.93. Even though average fare for rural drivers is higher compared to other city types, the total fares is significantly lower than in suburban or urban city types. 



Multiple line graph shows us relatively universal trends across all three city types with peaks and dips spaced more or less evenly from January to April. Notable exceptions - a peak and subsequent dive in urban fares throughout April comparing to dip and bounce in suburban and relatively steady decline in rural areas.

Our analysis showed that rural cities are the most underserved with the lowest amount of drivers. We recommend for PyBer to implement an incentive program to attract more drivers to better serve rural cities. To add more revenue across all city types we suggest introducing a loyalty program for regular customers as well as coupons for randomly selected customers and other rewards.
