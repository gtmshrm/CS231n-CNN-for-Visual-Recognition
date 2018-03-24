# Image Classification Pipeline

## Nearest Neighbour Classifier

**Algorithm**:

To train, Remember all training images and their labels. To predict, Predict the label of most similar training image.

**How to compare? What is the distance metric?**

There are many ways to compare: L1 distance: Manhattan distance, L2 distance: Euclidean distance, etc. We'll use L1 distance. The choice of distance metric is a hyperparameter. ![1](/lectures/img/lec_2/1.png)

## K - Nearest Neighbour Classifier

Find k similar examples from the training set with respect to test image and pick the class which has max vote

**Hyperparameters**: K, Distance metric

**Comparing K NN and NN**
![2](/lectures/img/lec_2/2.png)

### Finding hyperparameters

**Find hyperparameters which are K and distance metric in this algorithm**

* Cross-validation
