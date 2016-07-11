# Notes of MITx: 15.071x The Analytics Edge

This course is taught based on R and is relatively easy, but it is still worth taking. Here I listed some useful points that are not covered in the courses I have taken.

## An Introduction to Analytics

table()
>table uses the cross-classifying factors to build a contingency table of the counts at each combination of factor levels.

tapply()
>Apply a function to each cell of a ragged array, that is to each (non-empty) group of values given by a unique combination of the levels of certain factors.

## Linear Regression

out-of-sample R squared is used for testing and it can be negative.
```
SSE = sum((Y_test - Y_pred)^2)
SST = sum((Y_test - mean(Y_train))^2)
R^2 = 1 - SSE / SST
```

na.omit()
>na.omit returns the object with incomplete cases removed.

coredata()
>Generic functions for extracting the core data contained in a (more complex) object and replacing it.
>It can be used to avoid changing types such as using as.vector().
