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

**Probability Density Function** Works with Continuous Data. Gives the probability of a (continuous) data point falling within some given range of a given value.

**Probability Mass Function** Works with Discrete Data. Gives the probability of a (discrete) data point falling within some given range of a given value.

### Data Distributions

Open up the [Distributions Examples](/examples/Distributions.ipynb) notebook.

**Uniform Distribution** Has a flat constant probability of any value occouring. So the probability function would also be a flat line accross the range of the values. Outside of these values the line (probabilty) would be 0.

**Normal / Gaussian Distribution** Is generally a bell shape curve. Its possible to plot the Proability Density Function (PDF) for a Normal Distribution. See the Distributions.ipynb for details.

**Exponential PDF / "Power Law"** An exponential curve that generally has a high probability at the start and rapidly tapers off after.

**Binomial Probability Mass Function** Used for discrete values. It will present a shape similar to normal except the value will be 0 in between each discrete value and the spike up to >0 when a discrete value is in the X axis. There are shape parameters, n & p which can be used to change the shape of the distribution.

**Poisson Probability Mass Function** Shows the probabilty of getting a value on a specific day. So its essentially probaily of something happening at a particular time. Looks a bit like normal distribution curve.

### Percentiles & Moments

Open up the [Percentiles Examples](/examples/Percentiles.ipynb) notebook.

**Percentile** The point at which x% of the values are less than that value? For example, income distribution. Lets say the 99th percentile is $550K. That means that 99% of the population are earning less than that value (and 1% are earning more!). So the 50th percential is where half the population are making more than that and half are making more than that - it is right in the middle and is therefore also the median value!

**Quartiles** In a Normal Distribution, there are Q1 and Q3 in the middle of the distribution, together making 50% of the values split equally between Q1 and Q3 (25% each). The difference between Q1 and Q3 is called the 'Inter Quartile Range' (IQR).

Open up the [Moments Examples](/examples/Moments.ipynb) notebook.

**Moment** is the measurement of the shape of the distribution. There are 4 moments that we will consider. 

**First Moment** Is simply the mean.

**Second Moment** Is simply the varience.

**Third Moment** Is the **skew** of the data. Basically it is how 'lopsided' the distribution is (compared to a normal distribution) Its just stretching out the tail on one side or the other. There can be a **-ve skew** (longer tail on the left side) and a **+ve skew** (longer tail on the right side).

**Fourth Moment** Is the **kurtosis** of the data. Its basically how 'peaked' the distribution is (compared to a normal distribution). Its the measurement of the thickness of the tail and the sharpness of the tail.

### Matplotlib

Open up the [Percentiles Examples](/examples/MatPlotLib.ipynb) notebook.

**Multiple plots on one graph**

```
plt.plot(x, norm.pdf(x))
plt.plot(x, norm.pdf(x, 1.0, 0.5)) # the two params here are _mean_ and _standard deviation_).
plt.show()
```

**Custom Axis**

One you have the axis object use `set_xlim` and `set_ylim` to set the extents of each axis. Also use `set_xticks` and `set_yticks` to define exactly where the ticks on the axis appear.

**Line types and Colours**

```
plt.plot(x, norm.pdf(x), 'b-')
```

In the above example we can see that the `plot` function takes a third parameter which represents the color and the type of the line. In this example `b-` means **blue solid line**. Some more examples are:

* `b-` blue solid line
* `r:` red dotted line
* `g--` green dashed line

### Covariance and Correlation

Open up the [Covariance Correlation Examples](/examples/CovarianceCorrelation.ipynb) notebook.

A measurement of how closely dependent two values are related to each other.

Calculating covariance is quite involved so we will let python handle this for us. 

Interpreting covariance is hard. We know that a covariance close to 0 means there is not much correlation between the variables. However, for large covariances - far from 0 means there IS a correlation but how 'large' is large? This is where the correlation value comes to the rescue!

Correlation is the covariance divided by the SD of both variables which normalizes the value. 

Now we can say with confidence that a correlation value of:

* -1 = perfect inverse correlation
* 0 = no correlation at all
* 1 = perfect correlation

NOTE: That a perfect correlation does not imply causation (that one value directly affects the other). A controlled, randomized experiment is needed to make that conclusion.

Python functions are:

```
numpy.cov(x,y) # calculates the covariance
np.corrcoef(x,y) # calculates the correlation
```

### Conditional Probability

Open up the [Conditional Probability Examples](/examples/ConditionalProbabilityExercise.ipynb) notebook.

If we have two events that depend on each other what is the probability that both will occur?

**Notation**

* P(A,B) = Probability of A & B occuring independently of each other
* P(B|A) = Probability of B occuring given that A occured (implying a dependencey between B & A)
* P(B|A) = P(A,B) / P(A) **<- this is our formula!**

**Example**

I give my students two tests (A & B). 60% pass BOTH tests and 80% passed the FIRST test (A). What is the % of students who passed the first test also passed the second test (so what is P(B|A))?

Therefore:

* P(A,B) = 0.6
* P(A) = 0.8
* P(B|A) = 0.6 / 0.8 = 0.75

So the answer is 75%

### Conditional Probability Examples

Open up the [Conditional Probability Examples](/examples/ConditionalProbabilityExercise.ipynb) notebook.

In this example we have 100K people that are evenly distributed amoung 6 age groups (20s, 30s, 40s, 50s, 60s & 70s) in one [Python Dictionary](https://www.w3schools.com/python/python_dictionaries.asp) and have their purchase frequencies stored in another Python Dictionary as described below:

"totals" contains the total number of people in each age group. "purchases" contains the total number of things purchased by people in each age group. The grand total of purchases is in totalPurchases, and we know the total number of people is 100,000.

The two dictionairies might look like the ones below:

```
{20: 16576, 30: 16619, 40: 16632, 50: 16805, 60: 16664, 70: 16704} # totals dictionary
{20: 3392, 30: 4974, 40: 6670, 50: 8319, 60: 9944, 70: 11713} # purchases dictionary
45012 # total purchases
100000 # total population
```

So as you can see in the above two dictionaries, the `totals` is pretty much evenly spread (as intended, even though of course age population is not distributed like this!) and `purchases` is clearly depentent on the age group, with younger people purchasing less than older people (again as intended for this exercise). The code to generate this dataset is in the [Conditional Probability Examples](/examples/ConditionalProbabilityExercise.ipynb) notebook.

#### Exercise 1

Compute P(E|F), where E is "purchase" and F is "you're in your 30's". 

The probability of someone in their 30's buying something is just the percentage of how many 30-year-olds bought something. So, given the above dataset:

```
P(E|F) = float(purchases[30]) / float(totals[30])
P(E|F) = 4974/16619 = 0.29
```

#### Exercise 2

P(F) is just the probability of being 30 in this data set or the percentage of the total population who are in their 30s:

```
P(F) = float(totals[30]) / 100000
P(F) = 16619 / 100000 = 0.16
```

#### Exercise 3

P(E) is the overall probability of buying something, regardless of your age.

```
P(E) = totalPurchases / 100000
P(E) = 45012 / 100000
P(E) = 0.45
```

#### Exercise 4

If E and F were independent, then we would expect P(E|F) to be about the same as P(E). But they're not; PE is 0.45, and P(E|F) is 0.29. So, that tells us that E and F are dependent, the liklyhood of making a purchase and the age group of that person (which we know they are in this example).

So it makes sense to consider conditional probability! :)

What is P(E)P(F)?

```
P(E)P(F) = 0.45 x 0.16 = 0.072
```

#### Exercise 5

P(E,F) is different from P(E|F). P(E,F) would be the probability of both being in your 30's and buying something, out of the total population - not just the population of people in their 30's:

```
P(E,F) = float(purchases[30]) / 100000
P(E,F) = 4974/100000
P(E,F) = 0.049
```


#### Exercise 6

When E & F are independent of each other we can say P(E,F) = P(E)P(F). However, in our example they are not (P(E)P(F) = 0.072 & P(E,F) = 0.049). This is because they are dependent on each other. 

So instead we can rely on the formulae of conditional probability: P(E|F) = P(E,F)/P(F) and sure enough, it is:

```
P(E|F) = (purchases[30] / 100000.0) / P(F)
P(E|F) = (4974/100000) / 0.16
P(E|F) = 0.049 / 0.16
P(E|F) = 0.31
```

### Bayes' Theorem

Given conditions A & B then Bayes is the probabilty of A occuring given that B occurs and is based on this formulae:

```
P(A|B) = (P(A) * P(B|A)) / P(B)
```

The main insight is that the probability of something that depends on B depends very much on the base probability of B and A.

It also means that P(A|B) is NOT the same as P(B|A). 

So in a real word case the probability of someone being a drug user given they tested positive for the drug is NOT the same as someone who is a drug user AND testing positive for the drug.

#### Bayes' Theorem Drug Testing Example

We have a drug test that can accurately detect the presence or absense of the drug with 99% accuracy.

In this example 0.3% of the population are users of the drug.

* Event A = That you are a user of the drug
* Event B = That you tested positivly for the drug

So we need to calculate P(B). This is the probability of testing positive if you DO use the drug (= 0.99 * 0.003 = 0.00297) PLUS the probability of testing postive if you do NOT use the drug (= 0.01 * 0.997 = 0.00997)

Basically 0.3% use the drug so their test will have a 99% accuracy.
Then 99.7% do NOT use the drug so their test will produce a false positive 1% of the time.

```
P(B) = 0.00297 + 0.00997 = 0.01294 = 0.013
```

So now we have: 

```
P(A) = 0.003
P(B) = 0.013
P(B|A) = 0.99
```

Therefore, the probability of being a drug user given that you tested positivly for the drug is:

```
P(A|B) = (P(A) * P(B|A)) / P(B)
P(A|B) = (0.003 * 0.99) / 0.013
P(A|B) = 22.8%
```

So, even though P(B|A) is high (99%), the probability of the opposite being true P(A|B) is a lot lower (22.8%). This is mainly due to the fact that such a low number of the population are actually users of the drug in this case.

### Linear Regression

Open up the [Linear Regression Examples](/examples/LinearRegression.ipynb) notebook.

Fitting a straight line to a set of observations. Can then use this line to predict unobserved / new values. Its based on the % slope / gradient of the line + the y intercept (the point at which the line crosses the y-axis).

It works by using something called **least squares** or **ordinarliy squares** or **OLS**. This basically minimizes the error between each point and the line. This results in the formulae: 

```
y = mx + b
```

So in probability terms its like maximizing the likiehood of the observed data. Sometimes this might be referred to as **'maximum likelihood estimation'**

**Gradient Decent** is an alternate approach to linear regression. However, gradient decent is more appropriate when dealing with 3D data so usually least squares in the case of simple linear regression is the best option.

#### r-squared

**r-squared** or **coefficient of determination** measures how well the line fits the dataset. Essentially this measures the fraction of the total variation in Y that is captured by the model. So how well does your line follow the variation that is happening.

```
r-squared = sum of the squared errors / sum of the squared variation from the mean
```

The value for r-sauared will range from 0 to 1.

* 0 = your line does not fit at all (so bad!)
* 1 = your line fits perfectly (so very good!)

### Polynomial Regression

Allows for fitting a curved line to a set of observations. So essentially the Linear Regression is actually the first order or first degree polynomial (since the power of X in the equation `y = mx + b` is 1).

Second order polynomial function: `y = ax^2 + bx + c`

Third order polynomial function: `y = ax^3 + bx^2 + cx + d`

And so on with higher orders producing more complex curves.

#### Beware of Overfitting

Don't apply more degrees than you really need to fit your data with a polynomial. Try to visualize your fit. Also use calculate r-squared value and see if that indicates a good fit or not.

There are techniques called train/test that can detect overfitting that will be covered later.