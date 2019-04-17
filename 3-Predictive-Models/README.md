## Predictive Models

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

### Multivariate Regression

Open up the [Multivariate Regression Examples](/examples/MultivariateRegression.ipynb) notebook.

This is the case where you may have a set of data that relies on more than one variable that influences the data.

For example, predicting the price of a car based on its attributes, like body style, brand, mileage, age, doors etc.

This works by using coefficients for each factor. For example: 

`price = α + β1milage + β2age + β3doors`

In the formulae above each coefficient (β1, β2 etc) indicates how important each factor is (when all normalized). So as the coefficient tends to zero then this indicates that the factor is probably less important to the observation we are trying to predict.

### Multi-Level Models

The concept that the thing that you are measuring can be influenced by many factors. For example, the health of your cells is influenced by the health of your organs that contain the cells and the body which the organs are in and the home that you live in and the environment that might affect your stress or the pollution levels of the city,etc,etc. As you can see its possible to go up and up into different levels that can potentially affect the thing that you are measuring.

This is an advanced topic. More details can be found [here](https://en.wikipedia.org/wiki/Multilevel_model).