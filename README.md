# MachineLearning

## Main

**Background:** Credit risk is an inherently unbalanced classification problem, as the number of good loans easily outnumber the number of risky loans. Therefore, we need to employ different techniques to train and evaluate models with unbalanced classes. In this analysis we evaluate the performance of multiple models and made a recommendation on whether they should be used to predict credit risk.

**Oversampling**

First we compared two oversampling algorithms to determine which algorithm results in the best performance. 
We oversampled the data using the naive random oversampling algorithm and the SMOTE algorithm. 

The main paramenter of assessment will be using the F1 score. The F1 score, also called the harmonic mean, can be characterized as a single summary statistic of precision and sensitivity. The formula for the F1 score is the following:

2(Precision * Sensitivity)/(Precision + Sensitivity)

After printing the confusion matrix the F1 score is: **0.76.**  
```
                pre       rec       spe        f1       geo       iba       sup
  high_risk     0.01      0.58      0.62      0.02      0.60      0.36       104
  low_risk      1.00      0.62      0.58      0.76      0.60      0.36     17101

  avg / total   0.99      0.62      0.58      0.76      0.60      0.36     17205
```

Note: the model also predicts better the low_risk than high_risk, which is very concerning given that predicting the high_risk is more important that low_risk.

After printing the confusion matrix the F1 score is: **0.81** 
```
                   pre       rec       spe        f1       geo       iba       sup
  high_risk       0.01      0.49      0.69      0.02      0.58      0.33       104
  low_risk        1.00      0.69      0.49      0.82      0.58      0.35     17101

  avg / total     0.99      0.69      0.49      0.81      0.58      0.35     17205
```
Note: we observe the same pattern with low_risk predicted better than high_risk.

**Conclusion: SMOTE algorithm predicted a little bit better than naive random pversampling, however, the F1 score is not robust enough for this model to be span into a full commercial application.**

**Undersampling**

We then tested an undersampling algorithms to determine which algorithm results in the best performance compared to the oversampling algorithms above. We undersampled the data using the Cluster Centroids algorithm.

After printing the confusion matrix the F1 score is: **0.63**, **much lower model confidence compared to above.**
```
                   pre       rec       spe        f1       geo       iba       sup

  high_risk       0.01      0.58      0.46      0.01      0.52      0.27       104
   low_risk       0.99      0.46      0.58      0.63      0.52      0.26     17101

avg / total       0.99      0.46      0.58      0.63      0.52      0.26     17205
```
Note: we observe the same pattern with low_risk predicted better than high_risk.

**Combination (Over and Under) Sampling¶**

We finally tested a combination over- and under-sampling algorithm to determine if the algorithm results in the best performance compared to the other sampling algorithms above. We resampled the data using the SMOTEENN algorithm.

After printing the confusion matrix the F1 score is: **0.72**, **similar to oversampled but better than undersampled**
```
                  pre       rec       spe        f1       geo       iba       sup
  high_risk       0.01      0.68      0.57      0.02      0.63      0.39       104
   low_risk       1.00      0.57      0.68      0.73      0.63      0.39     17101

avg / total       0.99      0.57      0.68      0.72      0.63      0.39     17205
```

**Final Recommendation: all methods of sampling revealed a heavy bias/high precision towards prediciting low_risk applications vs high_risk applications, which is highly problematic when trying to catch those high_risk loans. Therefore, none of these models are recommended for commercial application unless model sensativities can be tweaked further.**

--
## Extention

We also trained and compared two different ensemble classifiers to predict loan risk and evaluate each model. We used the following modules: ```Balanced Random Forest Classifier``` and ```Easy Ensemble AdaBoost Classifier```, both from imblearn.ensemble. These modules combine resampling and model training into a single step. 

**Balanced Random Forest Classifier**

After printing the confusion matrix comparing for SMOTE the F1 score is: **0.94**
```
                  pre       rec       spe        f1       geo       iba       sup

  high_risk       0.03      0.71      0.90      0.06      0.80      0.63        82
   low_risk       1.00      0.90      0.71      0.95      0.80      0.65     17123

avg / total       0.99      0.90      0.71      0.94      0.80      0.65     17205
```

**Easy Ensemble AdaBoost Classifier**

After printing the confusion matrix comparing for SMOTE the F1 score is: **0.97**

```
                  pre       rec       spe        f1       geo       iba       sup

  high_risk       0.08      0.88      0.95      0.14      0.91      0.83        82
   low_risk       1.00      0.95      0.88      0.97      0.91      0.84     17123

avg / total       0.99      0.95      0.88      0.97      0.91      0.84     17205
```
**Conclusion: AdaBoost model shows the most reliable results and can likely be used in commercial application with some additional testing.**
