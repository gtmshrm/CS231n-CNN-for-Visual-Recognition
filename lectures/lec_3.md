# Linear Classification and Optimization

**Challenges in Visual Recognition**
[1](/lectures/img/lec_3/1.png)

**Goal**

* Define a *loss function* that qualifies our unhappiness with the scores across the training data.
* Come up with a way of effciently finding the parameters that minimize the loss function *(optimization)*.

## Multiclass SVM Loss
![2](/lectures/img/lec_3/2.png)

Here, we sum up over the incorrect class and we keep a safety margin of *1*. Safety margin means that if the score corresponding to the correct class is say *x*, then the scores of the other (incorrect) classses should be atmost *x-1*. Anything beyond that is bad.

*Interpretation for Multiclass SVM Loss*
![3](/lectures/img/lec_3/3.png)

For first image, correct class is *cat* and incorrect classes are *dog* and *frog*. Now, loss for this image is evaluated as 2.9 . The score of the correct class is 3.2 and all the incorrect classes can have a maximum score of 2.2 because the loss function has a safety margin of *1*. The *car* class has a score of 5.1 which is greater than (max score allowed for incorrect class) 2.2 by 2.9 and hence the contribution for loss by the *car* class is 2.9 . Since *frog* class has a score of -1.7 (which is less than the max allowed score i.e 2.2), it contribution is 0. Hence, for the first image, our unhappiness is 2.9 .
