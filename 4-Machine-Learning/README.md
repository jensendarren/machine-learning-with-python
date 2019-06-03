## Machine Learning with Python

Machine Learning is alorithms that can learn from observational data and make predictions from it.

Two different types of learning as follows:

### Unsupervised Learning

The model is not provided 'answers' it must make of the data by only observations. Clustering images of objects is a good example. So group by round vs. square objects or blue vs. red objects. The problem is that you don't know how the alorithm will behave and the output that it will produce. 

So why use this approach when there appears to be no real stucture or logic to the exercise? In some cases, unsupervised learnign can produce clustering outputs that were not even anticipated. This is one of the interesting benefits of using unsupervised learning - in the cases where you *don't know what you are looking for in the data set* (latent variables). With unsupervised learning one can 'tease out' these previously unseen clusters in your dataset.

#### Example 1: Dating Website: Characteristics of people who like eachother for dating

A dating application dataset might have some sterotypes of relations / clusting, however with unsupervised learning one can reveal interesting insights into the behvious of the users of the dating website that were otherwise not so obvious.

#### Example 2: IMDB: Movie properties vs. popularity

Movies have many properties and these might have some indication as to the popularity of the movie. Or they might have some other interesting clustering characteristic that is acatully very useful and interesting. 

#### Example 3: Product Descriptions vs. Prodcut Category

Every product has a description. What terms in a description have an influence on the actual product category? Some are obvious and some will be latent so we use unsupervised learning to find these out.

### Supervised Learning

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

### Bayesian Methods for detecting email Spam

Lets assume that it is likely that an email that contains the word 'free' is actually going yo be Spam. So that is the probability of the email being Spam given that it contains the word 'free' so `P(Spam|Free)`.

```
P(Spam|Free) = (P(Free|Spam)P(Spam)) / P(Free)
```

To calculate the P(Free) - the email simply containing the word 'free' is:

```
P(Free) = (P(Free|Spam)P(Spam)) + (P(Free|Not Spam)P(Not Spam))
```

#### What about all other words?

The above formula will only work with emails that contain the word 'free' but what about all the other words in the English language?

We can use *Naive Bayes* as follows:

Well what we can do is generate a `P(Word|Spam)` value for _every_ word in the English language during the training process (eliminating noise words like 'the', 'and', 'it', etc, etc). Then we would analyse the entire text of an email and run it though the formula and multiply the P values together to create an overall probability that an email being Spam.

This approach assumes the presence of different words is independant of each other.

#### Use Scikit Learn to make this easier

Open up the [Naive Bayes Examples](/examples/NaiveBayes.ipynb) notebook.

The approach is fairly simple as follows:

* We use `CountVectorizor` to work on lots of words at once.

* We then use `MultinomialNB` to do the heavy lifting for Naive Bayes calculations.

* We then train this on known sets of 'Spam' and 'Ham' emails (so this is basically an example of Supervised Learning).

Some of the code in the example:

```
vectorizer = CountVectorizer()
counts = vectorizer.fit_transform(data['message'].values) #Basically tokenizes the message to represent the number of times a word appears in the message. Splits each message into a set of words and the number of times each word appears. It actually converts the word into a number too btw!

classifier = MultinomialNB()
targets = data['class'].values
classifier.fit(counts, targets) #Creates the Naive Bayes model from the dataset
```
...and to test the classifier as follows

```
examples = ['Free Viagra now!!!', 'Lets play golf tomorrow?!']
example_counts = vectorizer.transform(examples) #Convert these test messages into the same format that we trained the model on.
predictions = classifier.predict(example_counts) #Ask the classifier which is spam and which is ham!
predictions
```

### K-Means Clustering

Open up the [KMeans Clustering Examples](/examples/KMeans.ipynb) notebook.

An unsupervised technique where we can take an amount of data and process it to find meaningful clusters in that data.

We split the data into K groups that are centered or groupd around around K centroids. Its unsuperviesed since this approach only uses the positions of the data points themselves and can sometimes find categories in your dataset that you did not even know would be there!

#### K-Means Clustering approach

Here is a basic guideline of the typical approach:

* Randomly pick K centroids (k-means)
* Assign each datapoint to the centroid its closed to
* Recompute the centroids based on the average position of each centroid's points
* Iterate until the points stop changing assignment to centroids

After that you can predict the cluster a new point belogs to by finding the centroid that new point is closed to.

Choosing the value for K is not so easy, however, the best approch is to choose a low value and keep increasing until you stop getting large reduction in squared errors. So if you see when you increase the value of K that the squared distances of the points to the centroids does not change to much then you probably have reached your limit of K at that point.

#### Watch out Local Minima!

You should also be aware of needing to avoid local minima. This means that the first low value of K that you select (or maybe near to that first value) yields a seemly good result set whereas in fact this is a localized discovery in the clustering of the data and it would therefore be well worth trying K at higher values to see if it yields anything different at these higher numbers.

#### Labling the clusters

This is something that only you can do! K-Means Clustering does not provide the solution to naming the clusters of data that it has found for you!

#### Python example

Below is the main part of KMeans clustering in Python - just two lines of code!

```
# Create a KMeans model with N clusters
model = KMeans(n_clusters=4)

# ... and ask the model to 'fit' the data into it! Very simple
# Note we scaling the data to normalize it! Important for good results.
model = model.fit(scale(data))
```

### Entropy

A measure of the datasets disorder - how same or different it is.

A low entropy tending towards 0 indicates that all the classes of the data are the same (homogeneous).

A high entroy indicates that the data classes are somewhat different.

### Decision Trees

A decision tree is a flowchart to help make decisions. We have a dependant variable like if we should play outside or not based on the weather. A decision tree is good choice since there are many parameters that influence the decision. A decision tree looks at all of the weather attributes such as sunny, cloudy, rainy etc.

Supervised learning can help generate the decision tree since we can feel a ML model with that data which contains all the weather paramerters and with the classification result - play outside or play inside?

#### Decision Tree Example

Lets say we are running a tech company and we need to hire. We can create a decision tree based on the content of the CVs of our current team so that we can predict the likelihood that a new applicant will be hired based on the content of their submitted CV.

The way we would do this is to create a table of interesting attributes that we feel contribute to the decision to hire that candidate. This could be: number of years experience, currently employed, number of previous employers etc, etc.

The resulting Decision Tree looks like this:

- **Did an intership?**
- Yes: Hire!
- No: **Currently Employed?**
    - Yes: Hire!
    - No: **< 1 prior employeer?**
        - Yes: DONT Hire!
        - No: **Attended a Top Tier School**
            - No: DONT Hire!
            - Yes: Hire!

#### How Decision Trees works.

Basically, at each step in the tree, find the attribute that we can use to partition the data set to minimizes the entropy of the data in the next step. So it produces the most efficient approach of making decisions since the entropy of the data is cleared out early on in the decision making process.

So in our CV example (above), the first step that comes out of the decision tree is if the candidate had an internship or not. This became the first decision in our tree because the next step after that contains a data set that has the least entropy out of all the other decisions.

Constructing a decision tree is all about finding attribute that returns the highest information gain (i.e., the most homogeneous branches).

The name of the algorithm that is used for generating Decision Tress is [ID3](https://medium.com/machine-learning-guy/an-introduction-to-decision-tree-learning-id3-algorithm-54c74eb2ad55).

Here is an article that [Explaines Decision Trees Easily](https://medium.com/@chiragsehra42/decision-trees-explained-easily-28f23241248) *but perhaps also goes into a little more detail!*

#### Random Forests

An issue with decision trees can be overfitting. Since the data set used for training works well only what that data set, it may not work so well with new data.

A solution is to use the Random Forest approach. This is where we create several decision trees from random subsets of the data and then have each tree 'vote' on the final decison based on the decisions from all the trees in the forest!

This approach is basically randomly re-sampling the input data for each tree. The term for this is *bootstrap aggregating* or *bagging*. We can also ramdomize a subset of the attributes each step is allowed to choose from. This results in more variation between tree to tree.

#### Decision Trees Exercise 

Open up the [Decision Trees Examples](/examples/DecisionTree.ipynb) notebook.

To read the output we have:

**Condition <= 0.5** (e.g. Employed? <=0.5): So if the **not employed** then follow the **left** path and if **are employed** then follow the **right** path. 

Now there can be some confusion becuase the data for Employed is 0 (FALSE) and 1 (TRUE) but the condition <= 0.5 when the value is 0 results in **true** (LOL!). So the decision trees always work by stating a true outcome to the condition statement means moving down the right path (even if, as in this case the actual answer to the question (Employed?) is **false**).

So each condition branches:

* Go left for *"true"*
* Go right for *"false"*

The **gini** score is a measure of entropy at each step.

The **samples** is the number of points that are being considered at this step that have not yet been sectioned off by a previous decision.

The **value** in the leaves is an indicator of [*not hired*, *hired*] outcome for that *sample*.

#### Ensemble Learning

Is where we combine multiple models together to make an overall prediction. Random Forests covered previously was an example of ensemble learning and so is K-means when we use several iterations of K to get the final output.

So its basically using multiple models to try and solve the same problem and let the models vote on the results.

Differnt types of basic ensemble learning are:

* **Bagging** Random Forest approach usese *bagging*. This is where many models are built on a randomly drawn from the subset of data.

* **Boosting** Is where each subsequent model in the ensemble boosts attributes that addresses data mis-classified in the previous iteration. So you build your model, you identify the weak points and then re-train by focusing (i.e. *boosting*) the attention of the training process on the attributes that were mis-classified in the previous iteration.

* **Bucket of Models** Using multiple different techniques and algorithms combined to generate new models. Analyse the results of each technique by testing the model and *pick the ONE model that works best*.

* **Stacking** Is similar to the *Bucket of Models* approach except in this case we **combine the results** of the all the models output together.

**NOTE:** There are more advanced techniques such as [Bayes Optimal Classifier](https://svivek.com/teaching/machine-learning/fall2018/slides/prob-learning/bayes-optimal-classifier.pdf), [Bayesian Parameter Averaging](https://www.coursera.org/lecture/bayesian/bayesian-model-averaging-adz4Y) & [Bayesian Model Combination](https://stats.stackexchange.com/questions/224015/how-to-implement-bayesian-model-combination) but these are mostly theroetical, computationally difficult to achive and mostly misunderstood so its better to use one of the simpler approaches listed above for ensemble learning.

#### Support Vector Machines (SVM) 

Clustering higher dementional data (i.e. data that has lots of different features). So if you a data set with multiple features that you want to predict with then SVM might be a good choice to help!

The approach finds higher-dimentional support vectors accross which to divide the data that define *hyperplanes* and is a supervised leaning technique.

**Kernel Trick** the kernel trick represents data in higher dimensional spaces to find hyperplanes that might not be apparent in lower dimensions. There are a variety of kernels that can be used that have various levels of computational cost depending on the problem and data set being used.

### SVM Example: Support Vector Classification

In practice you will use Support Vector Classification to classify data using Support Vector Machines.

As mentioned above, there are several 'kerels' that can be used with SVC and some will work better than others for a given data set.

Some examples of kernels that are available to use are:

* Linear Kernel
* RBF Kernel
* Polynomial (Degree N) Kernel

In the *Polynomial* example you can choose the value of N. Can also try ensemble learning as well.

Each of these has different computational requirements and needs a fair amount of careful configuration. Sometimes the more complex the analysis - the less accurate the data classification results.

### Recommender Systems

#### User-Based collaborative filtering

Based on your behaviour, interests, browsing and purchasing history as well as the actions of others - this system approach can be used to recommend products to the user.

* Build a matrix of things (basically a database table of users where the columns represent the item in question) that each user bought/viweed/rated. Maybe the schema is *User(id, category, product, rated?, purchased?, viewed?)*.
* Then, compute similarity scores between each user.
* Find users similar to you (or the person logged in).
* Recomend the things that the users similar to you bought/viweed/rated etc.

#### Problems with using user based collaborative filtering (CF)

It mostly boils down to the challenges of dealing with human nature, namely:

* People are fickle - their ideas and tastes change
* There are many more people than things. This basically means that focusing computational resources of recommending for Users is challenging since there are 7B people on the planet now, but not 7B movies, or music albums. So by that rational its better to focus on the similarities between products rather than users.
* People can do nasty things - basically meaning that people will always try to game the system.

#### Item-Based collaborative filtering

This means we are comparing items with one another - not people anymore. This solves a few issues like:

* A movie is always going to be the same movie - it does not change, its not fickle!
* There are fewer things than people (so less computation required)
* Its much harder to game the system.

The way this works is:

* Find every movie (or other) pairing that is watched by the same person.
* Measure the similarity of the ratings accross all users who watched both
* Sort by the movie and then similarity strength

So for example, take two films e.g. Star Wars and Empire Strikes Back, find people who watched both of these films, compare the rating that these people gave these films and if they are very similar then the movies must also be similar (in this example category).

There are other ways to do this, of course.

### Example using the Movielense data

Open up the [Naive Bayes Examples](/examples/SimilarMovies.ipynb) notebook and explore in there. Many useful tips and usage examples of the [Pandas](https://pandas.pydata.org/) library!