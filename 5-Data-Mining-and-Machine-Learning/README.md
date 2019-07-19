## Data Mining and Machine Learning

### K-Nearest Neighbor (KNN)

Given a set of data, classify new data points based on the 'distance' to new data.

So if we have a scatter plot of data and a new point (value) appears in the dataset then we can attempt to classify it based on its nearest 'K' neighbours.

Obviously the value of K will affect the classifiation that is selected. A higher value of K could cause outliers or values much further away to affect the result. So train/test technique can be applied to find an optimal value of K.

This is an example of Supervised Learning because its using a set of trained data of a known set of points and classifications to classify a new point.

Open up the [KNN (K-Nearest-Neighbors) Notebook](/examples/KNN.ipynb) notebook and explore in there.

Below is my personal review of the code:

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Jun  5 18:35:02 2019

@author: darren
"""

import pandas as pd
import numpy as np
import operator
from scipy import spatial

r_cols = ['user_id', 'movie_id', 'rating']
ratings = pd.read_csv('/Users/darren/workspace/learning/DataScience-Python3/ml-100k/u.data', sep='\t', names=r_cols, usecols=range(3))

# Group by movie id by the size (popularity) and mean rating
movieProperties = ratings.groupby('movie_id').agg({'rating': [np.size, np.mean]})

# Create a new dataframe and apply a function to normalize the size so that 0 means no one watched the movie and 1 is the most popular
movieNumRatings = pd.DataFrame(movieProperties['rating']['size'])
movieNormalizedNumRatings = movieNumRatings.apply(lambda x: (x - np.min(x)) / (np.max(x) - np.min(x)))

# Create a new dictionary and load in the genre meta data for that movie and include the name, normaized size (popularity) and the mean rating in the dictionary
movieDict = {}
with open(r'/Users/darren/workspace/learning/DataScience-Python3/ml-100k/u.item', encoding = "ISO-8859-1") as f:
    temp = ''
    for line in f:
        #line.decode("ISO-8859-1")
        fields = line.rstrip('\n').split('|')
        movieID = int(fields[0])
        name = fields[1]
        genres = fields[5:25]
        # This converts the genre values to ints as they are currenly string '0' or '1'
        genres = map(int, genres)
        # Here the dict contains a python tuple. The list call produces the output needed to create the np array.
        movieDict[movieID] = (name, np.array(list(genres)), movieNormalizedNumRatings.loc[movieID].get('size'), movieProperties.loc[movieID].rating.get('mean'))

# Create a ComputeDistance function.
def ComputeDistance(a, b):
    genresA = a[1]
    genresB = b[1]
    # Genre distance is based on a spatial cosine function distance
    genreDistance = spatial.distance.cosine(genresA, genresB)
    popularityA = a[2]
    popularityB = b[2]
    # Popularity distance is simply the difference between the two movies being compared
    popularityDistance = abs(popularityA - popularityB)
    return genreDistance + popularityDistance


# Create a getNeighbors function that takes a movieID and a value for K
def getNeighbors(movieID, K):
    distances = []
    for movie in movieDict:
        if (movie != movieID):
            # So for each movie (except the one we are comparing) compute the distance and append as a tuple with movieID to the distanes array
            dist = ComputeDistance(movieDict[movieID], movieDict[movie])
            distances.append((movie, dist))
    # sort by dist column
    # https://stackoverflow.com/questions/18595686/how-does-operator-itemgetter-and-sort-work-in-python        
    distances.sort(key=operator.itemgetter(1))
    neighbors = []
    # Simply get the K nearest neighbors from the distances array (since its sorted already)
    for x in range(K):
        neighbors.append(distances[x][0])
    return neighbors

K = 5
movieID = 50 # Star Wars
avgRating = 0
neighbors = getNeighbors(movieID, K)
for neighbor in neighbors:
    avgRating += movieDict[neighbor][3]
    print (movieDict[neighbor][0] + " " + str(movieDict[neighbor][3]))
```

## Curse of dimensionality

Many problems have several dimensions of data. For example the movie data set has many movies (100s in fact) so its said to have 100s of dimensiions of data. So every single movie can be tought of as a dimension in that data space.

Alterively you may have a dataset with many different features. For example the [iris flower dataset](https://en.wikipedia.org/wiki/Iris_flower_data_set) contains 4 features for each flower. So in this case there are multi-demensions: 100s of flowers each with 4 features: that's a lot of dimensions and difficult to wrap our heads around! The iris data set is included in sci-kit learn.

So a process called *dimensionality reduction* helps to distill higher-dimentional data down to a smaller number of dimensions while preserving the variance of the database. Similar approach might be used for compressing images. If you imagine that a black and while image is just a 2x2 grid of numbers between 0 and 1 (to represenent the brightness of each pixel) - X position, Y position, and brightness at each point. Then if this can be compressed into a smaller set, while preseriving that varience of brightness we can still represent the same image, more or less, when uncompressed.

An example of dimensionality reduction is K-means clustering (we covered earlier in the course). There is another (more sophisticated!) way, of course, and that technique is called:

## Principal Component Analysis

The approch finds higher dimensional planes in which to project the dataset onto while still preserving the variance in the data. A popular implementation of this is Singular Value Decomposition (SVD)

### Example: Visualizing 4-D Iris Flower Data

The 4 dimensions are: length and width of petals and sepals. We also know the subspecies classification of each flower.

Using PCA we can visualize this dataset in 2 dimensions, instead of 4, while preserving the varians.

Open up the [PCA.ipynb](/examples/PCA.ipynb) file and dig in!

In the exerciese we reduce the 4 dimensions down to just 2. You can see the three different types of Iris are still clustered pretty well. If you think about it, this probably works well because the overall size of an individual flower probably makes both the petal and sepal sizes increase by a similar amount. 

## Reinforcement Learning

Where we have an 'agent' that needs to explore an environment of sorts and as it travels around this environment the agent learns the value of different states in different conditions. A good academic example to apply this would be in a Pac Man game where Pac Man is the agent and the space is everything else - the maze, the ghosts, the fruit etc.

### Q-Learning 

A specific implementation of Reinforement Learning. This can also be refered to as Markov Decision Processes (MDPs) and is a _discrete time stochstic control process_. Reinforement Learning is also a form of _Dynamic Programming_.

This involves having:

* A set of environmental states *s*
* A set of possible actions in each state *a* (in Pac Man that are the possible moves up, down, left right)
* A set state/action pair *Q* (in Pac Man each state will have all the possible actions *a* and we assign a value *Q* to _each_ action for _each_ state.)

The value of Q starts of as 0 and as the agent explores the space, when a positive (good/rewarding) event occurs then _increase_ Q and when a negative (bad/unrewarding) event occurs then _decrease_ Q.

When using this approach we can obviously calculate Q for each current state. Again if something positive happpens for that action (like eating a 'power pill') then the value of Q can _increase_ and if its a negative event (like being killed by a ghost) then the value of Q can _decreate_.

It's also possible to 'look ahead' more than one step by using a discount factor when computing Q, like so:

Q(s,a) += discount * (reward(s,a) + max(Q(s')) - Q(s,a))

There is a challenge when exploring the environment. How most efficiently to do that?

**Simple Approach** - always choose the action for the given state with the highest Q. If there is a tie then choose at random. However, its inefficient and we could miss a lot of paths!

**Better Approach** - introduce a little randomness known as an _epsilon term_. Basically, if a random number is less than epsilon then **don't** follow Q, but instead choose a random path. That way, exploration never totally stops. However, choosing a value fo epsilon can be tricky.

Further exploration: 

https://pymdptoolbox.readthedocs.io/en/latest/api/mdptoolbox.html
https://inst.eecs.berkeley.edu/~cs188/sp12/projects/reinforcement/reinforcement.html