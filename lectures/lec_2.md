# Image Classification Pipeline

*Winter 2016*

## Nearest Neighbour Classifier

To train, remember all training images and their labels. To predict, find the label of most similar training image.

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

Some portion of the training set (say 16%) is considered as validation set. The hyperparameters which perform best on this validation set are selected.

#### Cross-Validation

![3](/lectures/img/lec_2/3.png)

In cross-validation, training data is divided into folds. In the following example we'll find K. We call also find distance metric (which is another hyperparameter) by the exact same technique which we use to find K.

Eg: Say 5 folds in this case. Lets name the 5 folds as F1, F2, F3, F4 and F5.

For K=1:

At first, consider F5 to be the validation set. Now the accuracy of the algorithm is calculated on F5. Let's call this accuracy as A5. Then F4 is considersed as validation set and accuracy on F4 is calculated i.e A4. Similarly, A3, A2 and A1 are calculated. In short, every fold gets to be the validation set. Now the average of A1, A2, ..., A5 is calculated. Let's call this average accuracy as A.

The above mentioned process is repeated for odd values of K (3, 5, ...) and for each K, we get A, A1, A2, ..., A5 where A is the average of A1, A2, ..., A5. All of these values are plotted as shown below. The line passes through A (mean accuracy) for odd values of K. The vertical bars indicate std dev for A1, A2, ..., A5 for each K.
![4](/lectures/img/lec_2/4.png)

Now, the K which gives highest mean accuracy obtained through cross-validation is selected. It is indicated by the vertical red line in the above graph.

Similarly, cross-validation can be used to find the distance metric. This is how we can find hyperparameters for any ML algorithm.

Cross-validation is expensive and hence, it is used prefarably for small datasets. Use validation instead of cross-validation for medium or big datasets.

**K-NN is never used on images**
* Computational performance at test time is terrible
* Distance metrics on level of whole images can be unintuitive. See example below.
![5](/lectures/img/lec_2/5.png)

## Linear Classification

Example of an image with 4 pixels and 3 classes (cat/dog/ship)

![6](/lectures/img/lec_2/6.png)

Each row of W and b is an independent classifier for corresponding class.

### Interpreting a Linear Classifier

![7](/lectures/img/lec_2/7.png)

As shown above, we reshape each row of weight matrix W into the dimensions of original input image (only for visualization). We can visualize each row of W as a 32x32x3 image. Lets consider the weights which corresponds to class 'plane' in the image above. We observe that the blue channel has lots of positive weights. When these positive weights of blue channel see blue sections in the input image, they interact with them to give a good contribution to the final score for class 'plane'. In red and green channels, we'll find weights which are close to zero and even negative. Weights for a class can also be called as a template for that class. The reason for weights of class 'plane' to have high blue channel values is because it might have seen a lot of blue sections on the training images.

Similarly, the weights for class 'frog' contain yellow green part in the center and brownish parts on the sides. When these parts see similar patterns of color in the input image, the dot product becomes high which gives a good contribution to the final score.

The weights for class 'car' look a bit weird because training set had images of cars with many different orientations. The weights of class 'horse' can be seen as double faced horse with the left face being darker because training set had more left faced horse images. Also, the color of horse in the weight vector seems to be brown but horses can be of any color. This is because CIFAR-10 has many brown horses.

*Trying to accomodate for both left and right faced horses in a single weight vector and bias of the classifier towards brown horses shows the lack of power in linear classifier. Of-course CNNs and Neural Nets in general have different weight vectors corresponding to each orientation of the horse.*

**Another interpretation of a linear classifier**

Using linear classifier on CIFAR-10 dataset, each class is linearly separated across the 3072 dimensional pixel space. This can be interpreted as shown below.

![8](/lectures/img/lec_2/8.png)
