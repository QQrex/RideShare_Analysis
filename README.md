# RideShare_Analysis

## Purpose

Create a summary of the PyBer data and a multiple-line chart of total fares for eacy city type in the PyBer rideshare data.

## Project Overview

-Create a ride-sharing summary DataFrame by city type
-Create a multiple-line chart of total fares for each city type

## Analysis

**[Pyber Summary]**

To start our analysis of our data, we need to add our dependencies and path our csv files to read.

![path](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/Load%20dep.PNG)

Our next step would be to merge our two csv files into one DataFrame in our script to easily access all fields in one DataFrame. We will pd.merge to merge on the 'city' column.

![merge](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/merge%20data.PNG)

Once we have one complete DataFrame, we will can count the total rides made per city type and total drivers per city type.

![count](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/counts.PNG)
>Cell 1 - Use .groupby on pyber_data_df to count all rider IDs by city type.
>
>Cell 2 - Use .groupby on city_data_df to sum all drivers by city type. We don't want to use the pyber_data_df because there are duplicate values of driver counts in pyber_data_df when we merged the two csv files. It is easier just to use the original city data csv file to find driver count by type.

Now we will need to caculate the total fares by city type and also figure out avgerage ride per rider and per driver.

![fare](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/fares.PNG)
>Cell 1 - Similiar to how to we calculated driver count, we will use groupby to sum fares in pyber_data_df per city type.
>
>Cell 2 - Divide total fare by total rider count to find average fare per rider.
>
>Cell 2 - Divide total fare by total driver count to find average fare per driver.

Finally, we can construct our pyber summary DataFrame.

![Pybersumy](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/pyber%20summary%20df.PNG)

**[Plot Line Chart]**

To create a multiple-line chart we need to create a piviot table with date (in weeks) as x-axis, fares (sum by dates) as y-axis and our lines as city types. To do this we first need to extract the relevate data from the pyber_data_df. We can use .groupby again but this time we group both type and date together to sum fare per city type with dates. Our new Series will show type and date as indices with sum of fares

![indexsum](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/index%20sum.PNG)

Next, we need to reset the indices in order to use .pivot to create a pivot table because the .pivot method cannot take multiple indices.

![resetindex](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/reset%20index.PNG)

Now we can use .pivot to create a pivot table with dates as index values, columns as types and values as fare. We would also like to narrow down on the range of dates we are looking at from 2019-01-01 to 2019-04-29.

![pivot](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/pivot%20table.PNG)
>Cell 1 - Create pivot table
>Cell 2 - Use .loc to only look at row values between 2019-01-01 to 2019-04-29

Our next step would be to group the dates by weeks. We could use .resample, however we need to check if our data type for our date index is in 'DatetimeIndex' type. If our data type is not right, we will have to to use pd.to_datatime to change the data type to 'DatetimeIndex'.

![datetime](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/datetime.PNG)

Now that our index data type is 'DatetimeIndex' we will use .resample to group the indexes by week and also sum their values.

![resample](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/resample.PNG)

Finally, we can plot the resampled pivot table using object-oriented interface method.

![plot](https://github.com/QQrex/RideShare_Analysis/blob/main/Resources/oo%20plot.PNG)

## Results

![df](https://github.com/QQrex/RideShare_Analysis/blob/main/Analysis/Summary%20DF.PNG)
>PyBer ride-share data summary

![cfig](https://github.com/QQrex/RideShare_Analysis/blob/main/Analysis/ChallengeFig.png)
>multiple-line chat

## Summary

In summary, we can see a large disparity in average fare prices for urban driver prices versus suburban and rural. This is in part due to a higher ratio of riders versus drivers. We can see this effect the average fare for riders as well, but instead higher prices for rural areas versus suburban and urban. Perhaps we should also consider looking at time of day PyBer receives higher rider count and add a surge charge during peak rider count to increase lower average driver fare in urban cities.
