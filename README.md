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
