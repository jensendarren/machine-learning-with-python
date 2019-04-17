## Machine Learning with Python

Machine Learning is alorithms that can learn from observational data and make predictions from it.

Two different types of learning as follows:

#### Unsupervised Learning

The model is not provided 'answers' it must make of the data by only observations. Clustering images of objects is a good example. So group by round vs. square objects or blue vs. red objects. The problem is that you don't know how the alorithm will behave and the output that it will produce. 

So why use this approach when there appears to be no real stucture or logic to the exercise? In some cases, unsupervised learnign can produce clustering outputs that were not even anticipated. This is one of the interesting benefits of using unsupervised learning - in the cases where you *don't know what you are looking for in the data set* (latent variables). With unsupervised learning one can 'tease out' these previously unseen clusters in your dataset.

*Examples 1: Dating Website: Characteristics of people who like eachother for dating*

A dating application dataset might have some sterotypes of relations / clusting, however with unsupervised learning one can reveal interesting insights into the behvious of the users of the dating website that were otherwise not so obvious.

*Example 2: IMDB: Movie properties vs. popularity*

Movies have many properties and these might have some indication as to the popularity of the movie. Or they might have some other interesting clustering characteristic that is acatully very useful and interesting. 

*Example 3: Product Descriptions vs. Prodcut Category*

Every product has a description. What terms in a description have an influence on the actual product category? Some are obvious and some will be latent so we use unsupervised learning to find these out.

#### Supervised Learning

Where we have dataset that we can feed into the model with the actual answers so that the model can 'learn' and improve.

So we have a set of data (e.g. car prices) that has a set of properties (milage, year, make, cylinders, doors, price) and we can train the model to predict the price of the car given a set of input parameters.

#### Train / Test

We use train / test approach to determine how good a model is.

Spilt the data 80/20 into the train / test set of data and use that accordingly.

One can measure the model's accuracy (using r-squared) by asking it to predict the values for the test set and compare that to the known true values.

For this to work best you need:

* A large enough dataset
* Select the dataset ramdomly
* This approach also helps to prevent overfitting

But sometimes this approach may not work but it can be controlled with ensuring the dataset is large and that the selection of the train/test sets is truely random.

One way to protect against overfitting is to use K-fold Cross Validation. This approch is basically to take multiple train sets of data and test each one of these against the *same* test slice of data.

* So may be you have a one large dataset and split that again into K randomly assigned segments, say 4. 
* Reserve one set as your testing set.
* Then you will run the training on all the remaining sets.
* Take the average of the K1 r-squared scores

#### Bayesian Methods for detecting email Spam

Lets assume that it is likely that an email that contains the word 'free' is actually going yo be Spam. So that is the probability of the email being Spam given that it contains the word 'free' so `P(Spam|Free)`.

```
P(Spam|Free) = (P(Free|Spam)P(Spam)) / P(Free)
```

To calculate the P(Free) - the email simply containing the word 'free' is:

```
P(Free) = (P(Free|Spam)P(Spam)) + (P(Free|Not Spam)P(Not Spam))
```

*What about all other words?*

The above formula will only work with emails that contain the word 'free' but what about all the other words in the English language?

We can use *Naive Bayes* as follows:

Well what we can do is generate a `P(Word|Spam)` value for _every_ word in the English language during the training process (eliminating noise words like 'the', 'and', 'it', etc, etc). Then we would analyse the entire text of an email and run it though the formula and multiply the P values together to create an overall probability that an email being Spam.

This approach assumes the presence of different words is independant of each other.

*Use Scikit Learn to make this easier*

Open up the [Naive Bayes Examples](/examples/NaiveBayes.ipynb notebook.

The approach is fairly simple as follows:

* We use `CountVectorizor` to work on lots of words at once.

* We then use `MultinomialNB` to do the heavy lifting for Naive Bayes calculations.

* We then train this on known sets of 'Spam' and 'Ham' emails (so this is basically an example of Supervised Learning).