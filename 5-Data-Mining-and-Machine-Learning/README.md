## Data Mining and Machine Learning

### K-Nearest Neighbor (KNN)

Given a set of data, classify new data points based on the 'distance' to new data.

So if we have a scatter plot of data and a new point (value) appears in the dataset then we can attempt to classify it based on its nearest 'K' neighbours.

Obviously the value of K will affect the classifiation that is selected. A higher value of K could cause outliers or values much further away to affect the result. So train/test technique can be applied to find an optimal value of K.

This is an example of Supervised Learning because its using a set of trained data of a known set of points and classifications to classify a new point.