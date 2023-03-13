## Enseble Models

The general idea is going to be, to instead of a very intelligent and sophisticated model, we use a multitude of simple models. This is advantageous considering, complex models are usually slow and in comparison, simple models are usually fast and therefore more easily distributed.

Typical models
	- Bagging - Bootstrap Agregation
	- Boosting
	- Stacking

## Bootstrapping

Bootstrapping is a process to better get insight on the shape of the data, it works in 2 steps:

1- Resample the sample data with replacement 
	This obtains a sample of the data with which we will evaluate the shape by creating a model

2- Repeat 1 until using the evaluations of the shapes of the samples we can create a model for the totality of the data

1 model might be biased but the combination of the models will never be biased.

# Bagging - Bootstrap Aggregation

Bagging is therefore a combination of Enseble models and Bootstrap, this works by combining the sample data and model creating with the weak models this leads to a new set of steps.

Procedure
	Sample with replication
	Train supervised weak models
	Verify its performance with data set
	Repeat procedure
	Aggregate the results

### Random Forest

The most common Bagging algorithm, in this case we use decision trees as the weak model as they are simple and fast to learn
In this case the Bootstrapping works by not only only selecting parts of the data but also only selecting only certain columns from the dateset, then we must take this subset and train the decision trees with this datasets.

The interesting part of the algorithm, is that even thought we are only using subsets of the datasets to train the trees, the resulting models can be good enough to evaluate the original data with good enough results.

Adding more trees is not always a good idea, we are just perfecting the model to the original data.

# Pasting

Essentially Baging without bootstrapping, in a nutshell it generates a set of models each fitted to different partitions of the train/test set, then these are combined to create a model more effective then the sum of its parts.

# Boosting

Similar to Bagging but insted of multiple models all in paralel, we use the results of a model as input to train the next model. In a nutshell the resampling comes from the result of the previous model.

## AdaBoost

an adaptive boosting model

1. assigns weights to each instance in the training set for each  classifier  
1. Trains a weak model  
2. adapts the weights of each sample according to the prediction  error (larger error => larger weight)  
4. Repeat steps 1-3 for a number of iterations

-- Aditional Things

## Gradient Boosting

-- TODO

## XGBoost

Extreme gradient boosting or XGBoost, is gradient boosting with regularization, allows for a better way of wightning the trees and optimizing the gain function, it also uses gradient descent for the learning process