# Image Classification Pipeline

## Nearest Neighbour Classifier

**Algorithm**:

To train, Remember all training images and their labels. To predict, Predict the label of most similar training image.

**How to compare? What is the distance metric?**

There are many ways to compare: L1 distance: Manhattan distance, L2 distance: Euclidean distance, etc. We'll use L1 distance. The choice of distance metric is a hyperparameter.
![1](/lectures/img/lec_2/1.png)

## K - Nearest Neighbour Classifier

Find k similar examples from the training set with respect to test image and pick the class which has max vote

**Hyperparameters**: K, Distance metric

**Comparing K-NN and NN**
![2](/lectures/img/lec_2/2.png)

As shown above, K-NN has much more smoother boundaries, is much more resistant to noise and outliers as opposed to NN.

### Find hyperparameters

In K-NN, hyperparameters are K and distance metric.

There are 2 techniques to find hyperparameters for any ML algorithm:

1. Validation

Some portion of the training set (say 16%) is considered as validation set.

2. Cross-Validation

Some portion of the training set (say 16%) is considered as validation set.
![3](/lectures/img/lec_2/3.png)
In cross-validation, data is divided into folds. Eg: Say 5 folds in this case.
Lets name the 5 folds as F1, F2, F3, F4 and F5.
At first, consider F5 to be the validation set. **NOTE**: In cross-validation, validation set is just for the name sake. Here validation set is simply not used.

