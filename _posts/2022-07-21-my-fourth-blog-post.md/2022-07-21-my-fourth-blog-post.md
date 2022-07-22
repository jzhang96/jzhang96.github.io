2022-07-21
================
Jiyue Zhang
2022-07-21

# Ensemble Learning: Random Forest Trees

I found Random Forest the most interesting method.  
The Random Forest basically split up predictor space into regions,
different predictions for each region.  
Classification tree if goal is to classify (predict) group membership,
for a given region, usually use most prevalent class as prediction.  
Regression tree if goal is to predict a continuous response, for a given
region, usually use mean of observations as prediction.

# Advantages

-   Simple to understand and interpret output  
-   Predictors don’t need to be scaled
-   No statistical assumptions necessary
-   Built in variable selection

# Example

``` r
#Obtain training and test sets
library(tree)
library(randomForest)
library(ggplot2)
set.seed(50)
train <- sample(1:nrow(diamonds), size = nrow(diamonds)*0.8)
test <- dplyr::setdiff(1:nrow(diamonds), train)
diamondsTrain <- diamonds[train, ]
diamondsTest <- diamonds[test, ]

#Get random forest model fit on diamonds data
rfFit <- randomForest(price ~ ., data = diamondsTrain, mtry = ncol(diamondsTrain)/3,
ntree = 200, importance = TRUE)
rfPred <- predict(rfFit, newdata = dplyr::select(diamondsTest, -price))
treeFit <- tree(price ~ ., data = diamondsTrain)
pred <- predict(treeFit, newdata = dplyr::select(diamondsTest, -price))

#Compare Root MSE values (root of test prediction error)
rfRMSE <- sqrt(mean((rfPred-diamondsTest$price)^2))
treeRMSE <- sqrt(mean((pred-diamondsTest$price)^2))
c(rf = rfRMSE, tree = treeRMSE)
```

    ##        rf      tree 
    ##  578.1225 1362.7847

From the output of RMSE value we can see a much smaller RMSE value of
the Random Forest trees one which means the model has been much more
improved by Random Forest trees method.
