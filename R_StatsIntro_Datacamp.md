## Types of Variable 

* Nominal (Discrete) - named values e.g Colour
* Ordinal (Discrete/Continuous) - ranked values e.g. Difficutly rating 
* Interval (Continuous) -  ranked values with equal distance e.g. 
* Ratio (Continuous) - ratio is same as interval but have a true zero e.g. Temperature in Kelvin

http://www.mpopa.ro/statistica_licenta/Stevens_Measurement.pdf

## Independent vs dependent variables 

* Independent is typically nominal (treatment type)
* Dependent is typically ratio (disease rate)

## Histograms

* Normal distribution - bell shape
* Not all distributions are normal 
* Look for positive and negative skews
* Remember the skew is where the tail is, not the peak 
* Bimodal is 2 peaks, 2 normal distributions in one histogram
* Uniform (platykurtic) distribution is rectangular shaped as consistent values 
* leptokurtic has small range of values and one big peak 

## Scales
* Z-scale standard in statisics 
* Makes better communication of results, easy to interpret
* Z = (RawScore-Mean)/StandardDeviation
* Mean Z score is always zero so easy to see what is above and below mean
* Percentile rank can be found from Z score e.g. 50% below 0 in z-score (as 0 is the mean)
 
## Summary Statistics
* Measures of Central Tendency
* Mean = sum of scores divided by number of scores
* Median = middle score
* Mode = score occurs the most 

* Median is preferred when extreme scores in distribution

## Measures of Variance
* Variance = sum of (score - mean) squared / number of scores (-1, see below)
* The minus 1 is used if its a sample and not a complete population
* Variance also known as means squares 
* Standard deviation = Square root of variance 


## Important R Functions

* c()
* mean()
* sum()
* length()
* head()
* tail()
* plot()
* abline()
* class()
* factor()
* str()
* describe()
* summary()
* mean()
* mode()
* median()
* var()
* hist() 
* scale() ##z scores 
* hist(verbal_baseline,main="Distribution of verbal memory baseline scores", xlab="score",ylab="frequency")
* subset(red_wine_data, red_wine_data$condition == "Argentina")
* subset(white_wine_data, white_wine_data$condition == "France")$Ratings
* par(mfrow = c(1, 2)) ##arranges histograms 
