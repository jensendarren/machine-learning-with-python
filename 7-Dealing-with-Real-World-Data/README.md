## Dealing with Real World Data

### Bias Variance Tradeoff

Essentially this is about overfitting and/or underfitting your model.

#### Bias

How far from the 'real' answer are your results. If they are 'on target' then the bias is low and if they are all to one particular side of the target answer then the results can be said to have a bias.

#### Varience

How scattered the predicted values are from the 'real' answer.

In many situations, you will find that you will need to trade bias vs varience by overfitting or underfitting your data.

So in the case of *underfitting* you may just have a straight line to represent a prediction of your dataset thereby having a *low varience* for the predictions and a *high bias* relative to each observation. 

In contrast, *overitting* the dataset you will join the data together thus have a *high varience* for the predictions and a *low bias* relative to each observation.

#### Error

The main thing to consider of course is reducing error. 

Error is a function of bias and variance as follows:

```
error = bias^2 + varience
```

For example, a complex model may have a high varience and a low bias and a simple model a low variance and a high bias. However, both may have the same error value.

### K-Fold Cross Validation

This is an expansion on the practice of *train/test* approach to fitting out model correctly. In this appraoch, instead of simply having 1 training data set and 1 testing dataset - we basically have K sets of training data and K sets of testing data.

So the process is:

1. Split data into K randomly assigned sets
1. Keep one of the sets assigned for test
1. Train the remaining K-1 sets and measure their performance against the test set
1. Take the average of the K-1 r-squared scores

This approach helps to reduce overfitting to a single train/test split.

## K-Fold Cross Validation Example

Open the [K-Fold Cross Validation Jupyter Notebook](/examples/KFoldCrossValidation.ipynb) and have a play around!