# Machine Learning with Python Udemy course notes

These are my course notes for the [Machine Learning with Python Udemy](https://www.udemy.com/data-science-and-machine-learning-with-python-hands-on/) course.

### Course Notes

Download from the course notes from the [Sundog site](http://media.sundog-soft.com/Udemy/DataScience.zip). Extract these files somewhere useful for you on your local computer.

### Install Canopy

The best way to setup a Python development evnironment is to install [Canopy](https://store.enthought.com/downloads/). NOTE: On Mac you will need to open the Security Settings and allow the application to install since Apple by default will not allow anything to install that has not been downloaded via iTunes.

### Open Canopy Editor and install pydotplus

Open the Canopy Editor by clicking the Editor link in the Canopy Home Screen. In the Python console window type:

```
!pip install pydotplus
```

Note that to run commands from within the Canopy Editor you must prefix with a bang(!). For example to see the version of Python `python --version` run the following in the Canopy Editor:

```
!python --version
```

### Open a iPython Notebook / Jupiter Notebook file


iPython Notebook files are files with the `.ipynb` extension. There are several of these in the files that were downloaded from the Sundog website in the Course Notes section above. Double click on the file `outliers.ipynb` which will cause Canopy to open the file in the default browser (running the Jupiter Notebook locally via localhost:8888).

Now practice some Python 101 exercises by opening the file `python101.ipynb`.

### Basic Python tips

Given a list as follows:

```
x = [1, 2, 3, 4, 5, 6]
```

We can slice the list in this way:

```
x[:3] # return first three elements (so 1,2,3)
x[3:] # return everything after first three elements (so 4,5,6)
```
Use the `extend` function to push onto the end of a list like so:

```
x.extend([7,8]) # [1, 2, 3, 4, 5, 6, 7, 8]
```

Use the `append` function to append a single element to the end of the list:

```
x.append(9) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Create a Tuple (basically an immutable list) by splitting a comma separated string like so:

```
(age, income) = "32,120000".split(',')
```

For other examples please refer to the `python101.ipynb` notebook.

### Introducing Pandas

Introduces "Data Frames" and "Series" that allow you to slice and dice rows and columns of information.

Check the `PandasTutorial.ipynb` file for working examples. Below are some specific notes.

```
%matplotlib inline 
import numpy as np
import pandas as pd

df = pd.read_csv("PastHires.csv")
df.head()
```

Note the first line of code `%matplotlib inline` denotes that matplotlib charts will be rendered within the notebook and not in a new window. The rest of this code is self explainatory.

* `head()` is a handy way to visualize what you've loaded. 
* `shape` property retuns # of rows and # columns
* `size` property returns # of rows x # columns
* `len(df)` returns the number of rows in a DataFrame
* `df['Hired'][:5]` extract the first 5 rows of the hired column
* `df['Hired'][5]` pluck the hired value in the 5th row
* `df[['Years Experience', 'Hired']]` returns all rows for 'Years Experience' & 'Hired'
* `degree_counts = df['Level of Education'].value_counts()` grabs counts of each distinct value for 'Level of Education'
* `degree_counts.plot(kind='bar')` plots a histogram of the servies degree_counts.

#### Pandas Exercise

Try extracting rows 5-10 of our DataFrame, preserving only the "Previous Employers" and "Hired" columns. Assign that to a new DataFrame, and create a histogram plotting the distribution of the previous employers in this subset of the data.

```
sldf = df[['Previous employers','Hired']][4:9]
sldf = sldf.sort_values(['Previous employers'])
sldf.plot(kind='bar')
sldf
```

### Types of Data

**Numerical Data** - a quantitave measurement. There are two typs of numerical data:

* Discrete Data - Basically Integers - like 1,2,3 (e.g. counts)
* Continuous Data - Basically Floats - has infinite possibilities (e.g. heights)

**Categorical Data** - a qualititave measurement that does not have a mathematical meaning (e.g. Gender, Race, Religion, Political Affiliation etc)

**Ordinal Data** - a mix of Numerical and Categorical Data (e.g. rating)

### Statistics Refresher

**Mean** is just the average. So add all values and divide by the count.

**Median** is the middle value in the sorted set. If there is no exact middle then take the average of the two mid values.

**Mode** is the most common value in the dataset.

**Variance** How spread is the dataset? What is the shape of the dataset? Known as 'sigma squared'. Specifically, it is **the average of the squared differences from the mean**. The reason why we square the diffences is so that -ve variances count as much as +ve variances otherwise they would cancel each other out. This also gives more weight to the outliers.

Note that if you have the entire dataset (entire population of data) then divide by N but if you have a _subset_ of the dataset (sample of the data) then divide by N-1 (see below).

* Population Variance - divide squared differences from the mean by N (the entire population)
* Sample Variance - divide squared differences from the mean by N-1

**Standard Deviation** This is the square root of the variance. This is known as 'sigma'. It is the way we can identify what is an outlier in our dataset. So if you are within 1 Standard Deviation of the mean then that is considered a 'typical value' with everything outside of that considered an outlier. 

So given a dataset of (1,4,5,4,8) which has a Mean of 4.4 and an SD of 2.24 so 1 SD of the Mean for this dataset is within the range 2.16 <-> 6.64 and any value outside of that range is an outlier.


