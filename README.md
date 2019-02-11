# SocialCops-Task
SocialCops data analysis task
Challenge 1: Agriculture Commodities, Prices & Seasons 
 
Aim: Your team is working on building a variety of insight packs to measure key trends in the Agriculture sector in India. You are presented with a data set around Agriculture and your aim is to understand trends in APMC (Agricultural produce market committee)/mandi price & quantity arrival data for different commodities in Maharashtra. 
 
Objective: 
1. Test and filter outliers. 
2. Understand price fluctuations accounting the seasonal effect 
  1. Detect seasonality type (multiplicative or additive) for each cluster of APMC and commodities 
  2. De-seasonalise prices for each commodity and APMC according to the detected seasonality type 
3. Compare prices in APMC/Mandi with MSP(Minimum Support Price)- raw and deseasonalised 
4. Flag set of APMC/mandis and commodities with highest price fluctuation across different commodities in each relevant season, and year.

# Methodology
## 1.	Outlier detection and Removal:
•	Multivariate outlier detection as by plotting the modal price as a function of crop type no outliers were found but on analyzing modal price of each commodity in different APMC some outliers were identified. A sample image is shown below:
![akole_bajri_outlier](https://user-images.githubusercontent.com/24448222/52572277-7e65e300-2e3d-11e9-9c7b-f1afb2edf5eb.png)

•	Outliers can be removed by many methods such as by calculating Z score as most of the data lies between 3 standard deviations of mean or Tukey’s Rule can be used which stated that the outliers are values more than 1.5 times the interquartile range from the quartiles either below Q1 − 1.5IQR, or above Q3 + 1.5IQR. 

•	The data point identified as an outlier need not to be an outlier and can have significant impact on the data if removed so to analyze that cook’s distance can be used which is useful for identifying outliers in the X values (observations for predictor variables). It also shows the influence of each observation on the fitted response values. An observation with Cook's distance larger than three times the mean Cook's distance might be an outlier.

•	I used tukey’s rule to remove outliers for both the datasets. As if the datapoint is out of bounds then that data point can be removed or its value can be replaced by boundary thresholds. A sample image is shown below:
![akole_bajri_outlier_removed](https://user-images.githubusercontent.com/24448222/52572276-7dcd4c80-2e3d-11e9-9be6-be50c7c869d4.png)

## 2.1. Seasonality detection
•	Seasonality is identified for each APMC cluster for detecting seasonality rolling window method was used and data is fitted with both additive and multiplicative method and the residue was calculated and then the autocorrelation function was calculated and the ACF of bith the models was compared to find the seasonality type. Method was referred form [Reference for seasonality detection](https://itsalocke.com/blog/is-my-time-series-additive-or-multiplicative/)
	
## 2.2.  Removing Seasonality
•As a time, series data has 3 parts as shown in the image above so to de-seasonalize the data we can Remove the calculated trend from the time series will result into a new time series that clearly exposes seasonality.
![sad](https://user-images.githubusercontent.com/24448222/52572133-1e6f3c80-2e3d-11e9-8832-e326be77afea.png)

	
## 3. Price comparison
•	Prices are compared after de-seasonalizing and were plotted and one such comparison is shown below:
![price_comaprison](https://user-images.githubusercontent.com/24448222/52572182-3941b100-2e3d-11e9-9aef-6065809a0791.JPG)

## 4. Highest Price Fluctuatuion
•	Variance was calculated for every type of commodity for each APMC and the top 20 commodities was selected from all the commodities and save in the form of a data frame.

