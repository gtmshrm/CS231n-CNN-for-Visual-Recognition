# Image Classification Pipeline

## Nearest Neighbour Classifier

**Algorithm**:

To train, Remember all training images and their labels. To predict, Predict the label of most similar training image.

**How to compare? What is the distance metric?**

There are many ways to compare: L1 distance: Manhattan distance, L2 distance: Euclidean distance, etc. We'll use L1 distance. The choice of distance metric is a hyperparameter.
![1](/lectures/img/lec_2/1.png)

## K - Nearest Neighbour Classifier

Find K similar examples from the training set with respect to test image and pick the class which has max vote

**Hyperparameters**: K, Distance metric

**Comparing K-NN and NN**
![2](/lectures/img/lec_2/2.png)

As shown above, K-NN has much more smoother boundaries, is much more resistant to noise and outliers as opposed to NN.

### Find hyperparameters

In K-NN, hyperparameters are K and distance metric.

There are 2 techniques to find hyperparameters for any ML algorithm:

#### Validation

Some portion of the training set (say 16%) is considered as validation set.

#### Cross-Validation

![3](/lectures/img/lec_2/3.png)

In cross-validation, training data is divided into folds. In the following example we'll find K. We call also find distance metric (which is another hyperparameter) by the exact same technique which we use to find K.

Eg: Say 5 folds in this case. Lets name the 5 folds as F1, F2, F3, F4 and F5.

For K=1:

At first, consider F5 to be the validation set. Now the accuracy of the algorithm is calculated on F5. Let's call this accuracy as A5. Then F4 is considersed as validation set and accuracy on F4 is calculated i.e A4. Similarly, A3, A2 and A1 are calculated. In short, every fold gets to be the validation set. Now the average of A1, A2, ..., A5 is calculated. Let's call this average accuracy as A.

The above mentioned process is repeated for odd values of K (3, 5, ...) and for each K, we get A, A1, A2, ..., A5 where A is the average of A1, A2, ..., A5. All of these values are plotted as shown below. The line passes through A (mean accuracy) for odd values of K. The vertical bars indicate std dev for A1, A2, ..., A5 for each K.
![4](/lectures/img/lec_2/4.png)
