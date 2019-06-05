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