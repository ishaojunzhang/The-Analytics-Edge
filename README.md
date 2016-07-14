# Notes of MITx: 15.071x The Analytics Edge

This course is taught based on R and is relatively easy. However, it is still worth taking because it is very practical and contains plenty of interesting data sets. Here I list some points that are new to me but extremely useful for future reference. I recommend this course to anyone who is interested in analytics.

## An Introduction to Analytics

`table()`
>table uses the cross-classifying factors to build a contingency table of the counts at each combination of factor levels.

`tapply()`
>Apply a function to each cell of a ragged array, that is to each (non-empty) group of values given by a unique combination of the levels of certain factors.

## Linear Regression

out-of-sample R squared is used for testing and it can be negative.
```r
SSE = sum((test$y - pred)^2)
SST = sum((test$y - mean(train$y))^2)
RSquared = 1 - SSE / SST
```
`subset()`
>Return subsets of vectors, matrices or data frames which meet conditions.

`step()`
>Select a formula-based model by AIC.

`na.omit()`
>na.omit returns the object with incomplete cases removed.

`sample.split()` in `caTools`
>Split data from vector Y into two sets in predefined ratio while preserving relative ratios of different labels in Y. Used to split the data used during classification into train and test subsets.

```r
spl = sample.split(data$class, SplitRatio = 0.7)
train = subset(data, spl == TRUE)
test = subset(data, spl == FALSE)
```

`coredata()` in `zoo`
>Generic functions for extracting the core data contained in a (more complex) object and replacing it.

It can be used to avoid explicitly transforming data types such as using as.vector().

`mice()` in `mice`
>Generates Multivariate Imputations by Chained Equations (MICE)

`complete()` in `mice
>Takes an object of class mids, fills in the missing data, and returns the completed data in a specified format.`

## Logistic Regression
definition of [sensitivity, specificity and accuracy](https://en.wikipedia.org/wiki/Sensitivity_and_specificity)

interpretation of auc
* The probability the model can correctly differentiate between a randomly selected parole violator and a randomly selected parole non-violator.
* The AUC of a model has the following nice interpretation: given a random patient from the dataset who actually received poor care, and a random patient from the dataset who actually received good care, the AUC is the perecentage of time that our model will classify which is which correctly.

`prediction()` in `ROCR`
>Every classifier evaluation using ROCR starts with creating a prediction object. This function is used to transform the input data (which can be in vector, matrix, data frame, or list form) into a standardized format.

`performance()` in `ROCR`
>All kinds of predictor evaluations are performed using this function.

```r
LogModel = glm(formula, data = train, family = "binomial")
pred = predict(LogModel, newdata = test, type = "response")
predObj = prediction(pred, test$class)
auc = as.numeric(performance(predObj, "auc")@y.vallues)
perf = performance(predObj, "tpr", "fpr")
plot(perf) # roc curve
```

Sometimes the accuracy will not improve a lot compared to a baseline prediction (always predicting the majority), but the model is still valuable since it gives more information and different cutoffs can be used in different situations. The quality of the model is mainly evaluated by auc.

##Trees
`rpart()` in `rpart` and `prp()` in `rpart.plot`

```r
tree = rpart(formula, data = train, method="class", minbucket=25) # classification
tree = rpart(formula, data = train, minbucket=25) # regression
prp(tree)
pred = predict(tree, newdata = test, type = "class") # labels
pred = predict(tree, newdata = test) # probabilities
predObj = prediction(pred[, 2], test$class) # for roc or auc
```

`train()` in `caret` and `e1071`
```r
# cross-validation for CART
numFolds = trainControl(method = "cv", number = 10)
cpGrid = expand.grid(.cp = seq(0.01,0.5,0.01)) 
train(formula, data = train, method = "rpart", trControl = numFolds, tuneGrid = cpGrid)
```

