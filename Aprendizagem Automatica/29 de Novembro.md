
# Feature Selection

In supervised learning one of the most important problems is the relevance of features,
- This refers to when we train our model with irrelevant features, 
- When features that not only arent usefull to the model but are actually harmful, 
- when data is missing from the dataset...

## Handling Varaibles

To solve the problem of relevance of features we need to improve the way we handle the variables in our data.
The handling of the variables is done by trying to simplify the dataset to the mininal set of relevant 
factors, this is done by trying to find the right number of independent varaibles.
If this number isnt achieved
- Too many independent variables -> Many columns may bias the results and find spurious correlations
- Too few indepdent variables -> We can be removing the collumn essential to solve the problem

One might ask why we dont just use all varaibles? The usage of all variables would be stopped by not only performance but also by somehting called The Curse of Dimensionality.

### The Curse of Dimensionality

The larger the number of dimensions, the more likely it is that each sample is closer to the edge of the N-Dimensionality space than to any  
other sample

# Aproaches to Feature selection

There are multiple ways to define the best feature to use

## Variance based Feature Selection

The concept of this type of selection is to use variable varaince as a way to predict its value, this can be exceptionally usefull whens ome varaibles have 0 varaince, indicating they are the ones we should use.

Many varaince models can be used for the calculation
 - Binary relationships
 - Pearson Correlation
 - Spearman Correlation
 - Mutual Information

This can be usufll but we must take into consideration that sometimes one vairable can be not related to another but be related to the combination of said varaible and another
Take for example X = Z + Y, X is related with Z + Y but not related with Z nor Y.

## Brute Force

This method is garanted to give the best combination of variables, regardless it is only pratical if used in smaller problems considering it is very demanding computationcal point of view.
It can be usually done in models who dont need to go thought the enitre data (ex.. Linear models, Naive Bayes).

## StepWise

This method depends on iteratively adding or subtracting features from the model with the intent of improving the accuracy of the model,  this can be done by
### Forward Checking
	We start with an empty model and in each iteration add a feature to the model trying to improve accuracy

### Backwards Checking
	We start with a full model and in each iteraation we remove a feature from the model trying to improve accuracy

## Using Ensemble methods

In this case we are trying to use multiple models to analyze which varibles are more relevant to the problem.???