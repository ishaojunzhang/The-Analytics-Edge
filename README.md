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
SSE = sum((Y_test - Y_pred)^2)
SST = sum((Y_test - mean(Y_train))^2)
RSquared = 1 - SSE / SST
```
`subset()`
>Return subsets of vectors, matrices or data frames which meet conditions.

`step()`
>Select a formula-based model by AIC.

`na.omit()`
>na.omit returns the object with incomplete cases removed.

`coredata()` in `zoo`
>Generic functions for extracting the core data contained in a (more complex) object and replacing it.

It can be used to avoid explicitly transforming data types such as using as.vector().

## Logistic Regression
definition of [sensitivity, specificity and accuracy](https://en.wikipedia.org/wiki/Sensitivity_and_specificity)

interpretation of auc
* The probability the model can correctly differentiate between a randomly selected parole violator and a randomly selected parole non-violator.
* The AUC of a model has the following nice interpretation: given a random patient from the dataset who actually received poor care, and a random patient from the dataset who actually received good care, the AUC is the perecentage of time that our model will classify which is which correctly.

`prediction()` in `ROCR`
>Every classifier evaluation using ROCR starts with creating a prediction object. This function is used to transform the input data (which can be in vector, matrix, data frame, or list form) into a standardized format.

`performance()` in `ROCR`
>All kinds of predictor evaluations are performed using this function.

Sometimes the accuracy will not improve a lot compared to a baseline prediction (always predicting the majority), but the model is still valuable since it gives more information and different cutoffs can be used in different situations. The quality of the model is mainly evaluated by auc.
