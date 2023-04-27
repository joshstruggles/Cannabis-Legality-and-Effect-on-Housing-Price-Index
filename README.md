# Phase-4-Project
## Cannabis Legality and Effect on Housing Price Index
Student: Joshua Ruggles <br>
Instructor: Morgan Jones <br>
Data Science Flex <br>
Date: 4/23/23<br><br> 

### Business Problem 
We have been contacted by a real estate agency to see if there is any relation between a bump in housing prices where cannabis has been legalized and if so, when and how much?


We will take into account the year that cannabis was legalized in the state in question and train an ARMA model on the stationary data (if applicable) of states that have legalized cannabis and see if there would be a bump in HPI for homes in states that have yet to do so, if they so choose to legalize.
<br> 
### Cannabis' effect on Housing Market
For this project we are looking at cannabis and its effect on the housing market in states that have legalized recreational use.
<img src="photos/map.png"  /><br><br>
<center>Image from nbcnews.com (November 2022)</center><br>
<img src="photos/us_political_map.jpg"  /><br><br>
<center>Odd how much these two images match up.<br>
Governing Magazine (2020)</center><br>

## There is data on all 50 states 

<br><br>
### Abbreviations explored and why we don't currently need them:
<br><br>
- FIPS: FIPS codes are the numbers used to identify geographic 
regions like countries, states and counties.

<br><br>
- Annual Change (%): This is great tracking information for our analysis but currently will not work with our model. Also, because our intentions are to visualize this information we can just use HPI against each year to visualize change. 

<br><br>
- HPI with 1990 base: The average of the Housing Price Index from the year 1900 to 2000. 

<br><br>
- HPI with 2000 base: The average of the Housing Price Index from 2000 to presumably 2022. 

### What we do need:
<br><br>
- HPI: Housing price index 
<br><br>
The House Price Index (HPI) is a broad measure of the movement of single-family property prices in the United States. Aside from serving as an indicator of house price trends, it also functions as an analytical tool for estimating changes in the rates of mortgage defaults, prepayments, and housing affordability. Generally speaking this is the most important data for our analysis. <br><br>
https://www.investopedia.com/terms/h/house-price-index-hpi.asp
<br>
### What states then have legalized recreational cannabis use? 
<br>

_According to the National Conference of State Legislatures, 21 states have legalized the adult use of marijuana for recreational purposes: Alaska, Arizona, California, Colorado, Connecticut, Illinois, Maine, Maryland, Massachusetts, Michigan, Missouri, Montana, New Jersey, New Mexico, New York, Nevada, Oregon, Rhode Island, Vermont, Virginia and Washington._  
<br>
From: https://www.cnet.com/news/politics/marijuana-laws-by-state-where-is-weed-legal/#:~:text=According%20to%20the%20National%20Conference,York%2C%20Nevada%2C%20Oregon%2C%20Rhode
<br>
For our purposes we will also need to know when each state legalized recreational use of cannabis by year. <br>

- Alaska: Q4 2014
- Arizona: Q4 2020
- California: Q4 2016
- Colorado: Q4 2012
- Connecticut: Q1 2023
- District of Columbia Q1 2014
- Illinois: Q1 2020
- Maine: Q4 2016
- Maryland: TBD (2023)
- Massachusetts: Q4 2016
- Michigan: Q4 2018
- Missouri: Q4 2022
- Montana: Q1 2021
- New Jersey: Q2 2022
- New Mexico: Q2 2021
- New York: Q1 2021
- Nevada: Q1 2017
- Oregon: Q3 2015
- Rhode Island: Q4 2022
- Vermont: Q4 2022
- Virginia: Q3 2021
- Washington: Q4 2012
<br>
## Time Series analysis of the HPI of states that have legalized recreational cannabis use 
<img src="photos/legal_states_list.png"  />
<br> 
Dickey-Fuller Test: Alaska's HPI
<img src="photos/Alaska_staitonary_data.png" />
<br> 
### Function for differencing 
Well that's great that we were able to walk through that process once. Let's make a function to lessen the amount of work we may have to do in the future for the remaining states.
<img src ="photos/function_for_differencing.png" />
<br> 
### Training data and Testing Data
We will split our training data into 80% of the data, testing the following 20% but let's add in a TimeSeriesSplit down the road here.
<img src="photos/training_testing.png" />

### ACF(Autocorrelation Function): Alaska
<img src="photos/ACF.png" />

### PACF(Partial Autocorrelation Function): Alaska
<img src="photos/PACF.png" />
<br>
### ARMA 
<img src = "photos/ARMA.png" />

### Testing 
<img src = "photos/Testing.png" />

### ARMA model after cross validation 
<img src = "photos/Testing_1.png" />

### Train/Test Split on national_arma
<img src = "photos/Train_test_national.png" />

### Arma model on national dataset
<img src = "photos/arma_national.png" />

### Testing on national dataset
<img src="photos/testing_national.png" />

### Predict into the future on national data
<img src ="photos/national_forecast.png" />

### Cannabis Legislation not yet passed 
<img src="photos/illegal_states.png" />

## Hypothesis testing #1: 
There is an observable effect on recreational cannabis legalization and raised HPI. We will try the first four states and separate them by region to measure if there is any effect.  
<img src="photos/national_df_2013.png" />

# Colorado: Q4 2012
<img src="photos/colorado_pct.png" />

# Washington: Q4 2012
<img src ="photos/washington_pct.png" />

## Maine & Massachusetts
<img src="photos/national_df_2017.png" /> 
<img src="photos/maine_pct.png" />
<img src="photos/massachusetts_pct.png" />

## Hypothesis testing #2: 
Generally speaking, HPI percentage change in states that have legalized recreational cannabis use are higher than states that have not. We will look at the previous 10 recorded years (excluding COVID-19) and see which group of states has the higher average percentage.
<img src="photos/legal_vs_illegal_pct.png" />

## Hypothesis testing #3: 
The initial roll-out of recreational cannabis legality seems to suggest that this happened first in states where the HPI percentage over the last 10 recorded years was higher than the national average. Can we then predict where recreational cannabis legality may move next and if so, is that based on HPI percentages?

# Business Suggestion #1: 
There is an implied change in our dataset regarding increased HPI percentage change and cannabis legalization. It is our suggestion to consider investing inside of that space (a state that has legalized recreational cannabis use) the year legislation is passed and to consider selling within 3 - 4 years of acquiring a property. 

* The earliest adopters of legalized recreational cannabis use experienced up to 4 years of HPI percentage change increase that was measured above the national average; _this could be due to other external factors._ <br>
* This data was taken from the first four states to legalize recreational use of cannabis in the following regions:<br><br>
    * West Coast: Washington 2012 - 2016 = 2.84% above national average 2012 - 2016<br><br>
    * Mountainous West: Colorado 2012 - 2016 = 3.72% above national average  2012 - 2016<br><br>
    * East Coast: Maine 2016 - 2020 = 0.57% above national average 2016 - 2020 <br><br>
    * East Coast: Massachusetts 2016 - 2020 = .06% above national average 2016-2020
    
    
    <br>
 # Business Suggestion #2: 

As of 4/23/23 recreational cannabis use is legal has become legal in Delaware. Our suggestion is to purchase properties, _now_. <br><br>

<img src="photos/delaware.webp"  /><br><br>
<center>Delaware Presidential Election Voting History<br>
270towin.com (2020)</center><br><br>

<img src="photos/delawaretrain_test_split.png" /><br>

While we cannot make any assumptions regarding HPI percentage change or even HPI, we can say that our forecasted prediction and test set report a positive change over the next three years. Our model predicts that in 2022 (not shown in data) the HPI will go up 20.42 points, in 2023 39.38, and in 2024 54.55. Our model has a standard deviation of 14.11. In the year 2025 however it appears that there will be a potential HPI recession.

<br>
## Delaware Legalizaiton: Successful

According to 'Millions in Revenue Anticipated from Legalizing Marijuana in Delaware', orignally published on January 25, 2021 by Delaware State Auditor Kathy McGuiness, RPh, CFE link: https://auditor.delaware.gov/wp-content/uploads/sites/40/2021/01/Marijuana-Special-Report-FInal-Report-2021.pdf<br> <br>


In short: Delaware is likely to see a 215 million dollar cannabis industry based on its adult population of 792,119 (2021), an approximated 13 percent use rate in the adult population, with an estimated annual user spending of $2080 


With legalization of recreational cannabis use having been successful this past weekend in Delaware and an understanding that the housing price index (HPI) historically ticks upward during times of legalization, our ultimate suggestion is to invest in Delaware properties, now and consider selling at peak within the next 3 - 4 years.
<br> 

## Business Suggestion #3: 

It would seem that political alignment of a state has something to do with legalization of recreational cannabis use; the following states have either historically or recently voted for a democratic presidential candidate and have bills actively or plans to draft bills for legalization of recreational cannabis use in the near future. Consider investing in these states, next. 

States to watch: <br>

- Minnesota: house is set to vote on a bill drafted on 4/20/23 https://www.cbsnews.com/minnesota/news/420-legalized-cannabis-vote-minnesota-house/<br><br>

- Wisconsin: state GOP lawmakers set to work on cannabis legalization https://apnews.com/article/wisconsin-medical-marijuana-legalization-republicans-92a5764d72a54914ecee54b37d6e8d5b<br><br>

- Georgia: 2020 was the first year since 1992 that Georgia has voted democrat, there is a growing movement for recreational cannabis legalization via https://norml.org/georgia-marijuana-legalization-effort/ 


<br> 

# Conclusion

In conclusion, the data suggest that there is in fact a relationship between states that have legalized recreational cannabis and elevated HPI. 
<br><br>
It is our suggestion to purchase property in states that have legalized recreational cannabis in the same year that it was announced. 
<br><br>
Also for consideration, states that are considered ‘blue’ are also the most likely to also be considered a ‘green’ state.  






