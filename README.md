
# Max Miller Module 1 Final Project


## Introduction

In this project we were given a large set of house sales data from Kings county Washington from 2014/15 and given the opportunity to explore it and create a model/regression to predict house price based on any relevant sets of data.


## Final Project Summary

Our dataset included numerous variables that intuitively ought to be well connected with house price: house/apartment size (as measured in square feet of living space as well as lot size), number of beds/baths, measures of the house's condition, flags for various house features (like waterfront view) and house location (in the form of zipcodes and latitude/longitudes for each house).

After cleaning up the data and rendering some of the variables into more useful forms (I turned a spotty and incomplete list of 'last renovation year' into a simple flag for whether the house had had a renovation any time in the last decade or not, which proved to have real predictive power), I focused my attention on trying to get the most robust set of neighborhood related variables into my model without running into overfit issues.

It makes a certain intuitive sense that neighborhood should matter. This is born out by considering house prices overlaid on a map. Here, I have this data presented in two ways. 1) unadjusted - simply heatscale referring to house price. and 2) adjusted - actually showing the model error using a 'naive' model that considers things like house size and condition but not location.

![alt text](https://github.com/max-miller/Project-1/blob/master/unadjusted%202.png?raw=true "Unadjusted house prices")

![alt text](https://github.com/max-miller/Project-1/blob/master/adjusted%202.png?raw=true "Model errors plotted")

Lower price greens and purples in the above map suddenly become higher [relative] price yellows and oranges below. These are small houses or apartments that the naive model thinks should be cheap, but are more expensive than otherwise expected due to neighborhood effects.

Or consider a graph like this one below, which plots square feet of living space against house price for three zipcodes, suggest that there are some important neighborhood effects in play:

![alt text](https://github.com/max-miller/Project-1/blob/master/living%20price%20by%20zip.png?raw=true "House square footage against price")

On the one hand, the clear intuitive trend that you expect is there: larger houses are more expensive regardless of zipcode. Two other things are in play though. 1) some zips seem more expensive than others and, crucially, 2) the size of the square foot effect appears to differ by zip code. An extra square foot of living space appears to be more expensive in zip 98112 than in 98002.

The possibility for there to be different effect magnitudes between meaningful subsets of the data (like neighborhood or zip), suggests that this sort of house data may be best modeled with the inclusion of interaction terms between zipcode and some of the other variables or in the form of a multi-level model. As more variables are added, however, the possibility for over-fitting increases. Is our data here robust enough to support that many variables?

The short answer is that, based train/test splits that I performed on a series of progressively variable laden models, we have enough data here to support a model with dummies for the key independent predictors (house size, condition, recent renovation, etc.) the 70 different zipcodes and for interaction terms between zipcode and square feet of living space. There is, however, not enough data to support a multi-level model that incorporates interactions between all of the predictors and zipcode. There are, afterall, only around 21,000 pieces of data, split among 70 zipcodes. The smallest zipcode only has 50 points in it!
