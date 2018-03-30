# Linear Classification and Optimization

*Winter 2016*

**Challenges in Visual Recognition**
![1](/lectures/img/lec_3/1.png)

**Goal**

* Define a *loss function* that qualifies our unhappiness with the scores across the training data.
* Come up with a way of effciently finding the parameters that minimize the loss function *(optimization)*.

## Multiclass SVM Loss
![2](/lectures/img/lec_3/2.png)

It is know as *hinge loss*. Here, we sum up over the incorrect class and we keep a safety margin of *1*. Safety margin means that if the score corresponding to the correct class is say *x*, then the scores of the other (incorrect) classses should be at-most *x-1*. Anything beyond that is bad.

*Interpretation for Multiclass SVM Loss*
![3](/lectures/img/lec_3/3.png)

For first image, correct class is *cat* and incorrect classes are *dog* and *frog*. Now, loss for this image is evaluated as 2.9 . The score of the correct class is 3.2 and all the incorrect classes can have a maximum score of 2.2 because the loss function has a safety margin of *1*. The *car* class has a score of 5.1 which is greater than (max score allowed for incorrect class) 2.2 by 2.9 and hence the contribution for loss by the *car* class is 2.9 . Since *frog* class has a score of -1.7 (which is less than the max allowed score i.e 2.2), it's contribution is 0. Hence, for the first image, our unhappiness is 2.9 .

*Q1*. What do we use *1* as the safety margin?
*Ans*: We need a safety margin to keep the correct class's score greater than the incorrect classes. The scores are arbitrary which means their magnitude doesn't has an interpretable meaning. Since the scores are arbitrary, *we can use any arbitrary number as the safety margin*, but we use *1* simply because it's the smallest positive integer.

*Q2*. Why don't we use mean instead of sum in the loss function?
*Ans*: Mean can also be used instead of sum. But if we use mean we would be dividing the sum by the number of classes (which is constant). *Dividing loss function by a constant everytime would be useless*.

*Q3*.What if the sum was over all the classes (including *j=y_i*)?
*Ans*: In *j=y_i*, it add *1* in our loss. *Adding a constant to the loss everytime would be useless*.

*Q4*. What if we use

![4](/lectures/img/lec_3/4.png)

*Ans*: It is known as the *squared hinge loss*. The type of loss we use is simply a hyperparameter and we end up using the one which works better for our dataset. In most cases, hinge loss outperforms squared hinge loss.

*Q5*. Usually at initialization, *W* are small numbers, so all *s ~= 0* . What is the loss?
*Ans*: *Loss ~= N-1* where *N* is the number of classes.

**Sanity check for hinge loss implementation**: As suggested by *Q5*, the loss at initialization should be around *N-1* where *N* is the number of classes.

**Full training loss**

It is the mean of losses on all the examples

![5](/lectures/img/lec_3/5.png)

**Q. But there is a bug in our loss (show below). Suppose that we found W such that L = 0 (ignoring bias term for simplicity). Is W unique?**

![6](/lectures/img/lec_3/6.png)

**Ans**: *No*. Because we can scale *W* by some factor and still get the same *0* as loss. See the example below in which we scale the weights by 2 and still get *0* loss.

![7](/lectures/img/lec_3/7.png)

Now we can have multiple (optimized) values of *W* which give the same loss. There is a subspace of *W*'s which work equally well.

*This is not a nice property to have! This is why regularization comes into picture...*

### Weight Regularization

It is nice to have an unique *W*. Regularization function makes sure *W* looks nice! Here nice means *W should be unique and should not overfit the training set by keeping the weights small*.

![8](/lectures/img/lec_3/8.png)

Now we have to parts of the loss function. In our new loss function, main part of it is trying to find optimal value for *W* and the regularization part is trying to keep *W* nice. So the main part and the regularization part fight with each other during training because we want to simultaneously achieve both these objectives: optimize *W* and also keep it nice! Even if this makes the training error worse, it will perform better on test set.

**L2 Regularization: Motivation**

![9](/lectures/img/lec_3/9.png)

*Q*. Which weight will L2 regularization favor in the above problem? *w1* or *w2*?
*Ans*: It'll favor *w2* because it has better *statistical distribution of weights across the vector* i.e weights are spread throughtout the vector. Intuitively that means the classifier will take into account all the features of the input vector as compared to *w1* which only takes the first element of input vector into account.

## Softmax Classifier (Multinomial Logistic Regression)
