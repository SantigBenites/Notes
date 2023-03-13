## Problems with vectors

The way we have approached are models is flawed because not all data can be represented by a vector
To solve this problem we can resort to a new way of representation data, this being vector spaces and metric spaces. In the first one, we represent each instance as a set of features and their presence. The second one, we define instances in relation to other instances by use of a distance function.

## Distance Functions

- Euclidean Distance
- Manhattan Distance
- Jaccard Distance
- Cosine Similarity

## K - Nearest Neighbours

This model works by associating a value to a instance depending on the neighbours of said instance. This model works with the metric spaces we referred earlier. 
Can be used for regression and classification.
Doesn't require training considering the data is the model.

### Classification

Using KNN for classification can lead to ties, even when K is odd.
And with the increase of K the more homogeneity we will have among the data.

### Regression

Using KNN for regression, usually works by using the mean of k neighbours to make predictions, which will lead to small step increases.
In this model sometimes it usufull to apply different weights to k neighbours depending on distance.
KNN is being nature slower than most of the supervised learning, regardless it is very simple to parallelize and moreover there are multiple strategies to improve performance such as usign Nearest Neightbor algorithms and No NN algortithm, that may miss some values but its good enough.

### Ball Tree Search

A diferent aprach to KNN, where around every point we apply a radius, and only search for points inside this radious, the biggest advantage is that this aprach minimizes the distance calculations between points.

## Scaling data

Scaling data is sometimes nessecary, considering some models only work with sacled data. Scaling data usally means, formating data so that it restracts the existance of outliers.
To scale data, we must change the data so that out data fits in with the trainign set, this process need to be made for all data we want to use in our model.

### Data Scaling tecniques
- Standartization
- Range Scaling
- Power Transform
- Unit norm scaling
- Custom Scaling


## Handling missing Values

When a value is missing from the data there are 4 primary aproaches 
- Do nothing
- Eliminate the row
- Eliminate the column
- Input the data