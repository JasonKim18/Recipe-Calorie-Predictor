# Recipe-Calorie-Predictor

by Jason Kim

## Project Overview

This project is for DSC 80 at UCSD. The dataset that we used is from [food.com](https://www.food.com) and contains recipes and reviews from 2008. Additionally, Our exploratory data analysis on this dataset can be found [here](https://jasonkim18.github.io/Food-Analysis/).

## Framing the Problem

The prediction problem that we will be exploring is **predicting the amount of calories in a recipe.** This is a regression type of problem as we are trying to determine a continuous variable. The response variable 

The response variable that we are predicting is calories and this is a continuous quantitative variable. The amount of calories that are present in a recipe is something that a lot of people find to be important so I chose this variable to make predictions on.

The most common evaluation methods for a regression analysis are r-square, mean square error, and mean absolute error. For this analysis, we will be using the mean absolute error that will allow us to find the absolute difference between the predicted and the actual values. This statistic is pretty easy to understand and also isn’t influenced as heavily by any potential outliers in our data. If we weren’t so concerned about outliers, we could use the mean square error, but the squaring process means that outliers are weighted more heavily.

The information known before we make our predictions include the number of minutes it takes, the number of steps, number of ingredients, as well as other nutrition information that is posted on the recipe beforehand. 

## Baseline Model 

Our baseline model for predicting the amount of calories in a recipe used a simple linear regression model. The features used for this part were "minutes," "n_ingredients," and "total fat." Among these, they are all quanititatve as they all represent numerical values. As such, there was no need to use any encodings as they were all quantitative. However, we did have to standardize our values to make sure that they were weighted appropriately.

For our performance, we found the mean absolute error as well as calculating the accuracy score of our model. 

Mean absolute error of training data: 130.29070533170452 
Mean absolute error of testing data: 135.33617028374928

Our mean absolute error and scores indicate that our baseline model isn’t too great at predicting the actual caloric values for each recipe as the mean absolute error increases for the testing data and in general are very high values.

## Final Model 

For the final model, we added additional features for our model to take into consideration, which were: "sugar," "sodium," "protein," "saturated fat," and "carbohydrates." I chose these for the data and the prediction task as they are additional features and contain relavent information about the recipe that can be used to better calcualte the amount of calories in each recipe. A model can’t get worse by looking at additional features so we will look through all of them to see which ones have the most influence in predicting. Additionally, we also standardized these variables so the results wouldn’t be skewed or biased.

The modeling algorithm that I chose was the decision tree regressor as they help to capture the relationship between features. I the  used GridSearchCV to better tune the decision tree regressor. The hyperparamaters that U tuned were max_depth, min_samples_split, and min_samples_leaf. And these were the results of the best parameters that we found:
{'regressor__max_depth': None, 'regressor__min_samples_leaf': 4, 'regressor__min_samples_split': 10}

And again, the model's performance was evaluated using the mean absolute error. Our final model is an improvement over our baseline mode’s performance as the inclusion of these additional features helped to lower our mean absolute error substantially. The mean absolute error of the training and testing data went from 130.29070533170452 and 135.33617028374928 to 13.978586792791912 and 27.485060250672998 respectively.

## Fairness Analysis 

The question that we asked for this portion, was if our final model was fair for recipes that took longer than 100 minutes as with recipes that took less than 100 minutes. 

Our groups were as follows:
	Group x: recipes with over 100 minutes
	Group y: recipes with less than or equal to 100 minutes

The evaluation metric that we chose was the root mean squared error as we are using a linear regression model.

**Null Hypothesis:**
Our model is fair. The model's RMSE for recipes with more than 100 minutes is equal to the model's RMSE for recipes with 100 minutes or less.

**Alternative Hypothesis:**
Our model is unfair. The model's RMSE for recipes with more than 100 minutes is different than the model's RMSE for recipes with 100 minutes or less.

The test statistic that we chose was the differnece in the root mean squared error between the two groups. 

Our significance level was at alpha = 0.05 and the resulting p-value was 0.001. Thus, since our p-value(0.001)  is less than our alpha (0.05), we reject the null hypothesis. Thus, it it is very likely that there is a significant difference in RMSE between recipes with more than 100 minutes and those with 100 minutes or less. As a result, we conclude that our model is likely to be unfair and biased against recipes that take longer than 100 minutes to cook.
