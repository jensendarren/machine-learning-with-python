## Machine Learning in the Real World

### Deploying models to real time systems.

Design, programming, testing and training can be done using our local machines on Pythpn Jpyter Notebooks for example. What these produces is a model which generally we can call predict on.

To share this model with the world, so that other users can benefit somehow from the model we need to deploy that somewhere so that it can become accessible via a web or a mobile application.

The model could be deplpoyed to a web service and RESTful endpoints provided so that the client applications can push feature data to the service to then make predictions using the deployed model and the provided feature data.

## Example Google Cloud

There is an `externals` package in scikit-learn that essentially can export or dump out the model to a file. Below is a code snippet of doing that:

```
from sklearn.externals import joblib
joblib.dump(clf, "model.joblib")
```

Now simply upload the dumped `model.joblib` file to Google Cloud Storage and specifiy the `scikit-learn` framework.

Google Cloud ML Engine will magically expose a REST API to your uploaded model so that you can call it from client applications to make predictions in real time.

Exposed Classifier (model.joblib) -> Cloud Storage -> Cloud ML Engine <- REST APIs -> Client Application

## Example AWS

A larger example, this time with AWS. For example a recommender enginge. High level this could be:

Logs -> Kinesis -> S3 -> EMR -> Dynamo DB -> Lambda -> API Gateway <- REST -> Client Apps

To explain the above flow:

**Left to right** the data flows from some system logs via Kinesis into S3. This is then processed in realtime by Apache Spark running on AWS EMR. Predictions for users can be made in real time and results stored in Dynamo DB.

**Right to left** the client app requests recommendations for user id and makes a GET request via API Gateway to the Lambda which in turn connects to and fetches the recommendations from Dynamo.

## A/B Testing Concepts

A controlled experiment to measure the affect on a change in a web or mobile application has on user behaviour. You can test, design changes (color, layout), UI flow, pricing changes etc.

**How do you measure converson**

What is it that you want to drive with the change that you are testing. Main thing to do is speak to the business owners of the section that they are trying to optimize and ask them exactly what it is. For example, it could be order volume, amounts, profit, ad clicks etc.

However, to attribute actions downstream can also be hard. For example, one change may (or may not) affect other pages in the application. How to attribute that?

So you might change the color of a button on Page A, then user navigates to Page B and does something and then makes a purchase on Page C. What affect on the decision purchase did the change on Page A attribute to that? Should you discount the affect depending on the distance from the change to the action? Should we discard this entirely since they (may not) be related? It's complicated and important to get this right and not fudge results too much at the end of the day.

**IMPORTANT NOTE: Variance is your Enemy!**

 Main thing is about the sample size. If you run a short experiement and see that a change B performs better (say there is a hihger average spend) than the orginal site B then this is not conclusive that B is better than A over a small experiment.

 For example, the group that see B have a higher average purchase amount than the group that saw A, BUT the number of purchases overall is quite low and what you could be seeing is just the random variationin the order amounts to begin with (i.e. between group A and group B). Because they are going to be different _anyway_ weather you run the experiment or not....

 One way to address this issue is to examine conversion metrics with less varience. For example, order quntities vs. order dollar amounts.

 ## Determining Significance: Using T-Tests and P-Values

 So how to really determine if the results of an A/B test is 'real' (justified) or if it is a results of random variation? T-Tests and P-Values are an approach to help solve this!

### The T-Statistic

Measure of the difference between the two sets expressed as standard error where the size of the difference relative to the variance in the data.

A HIGH T value means there is probably a real differenece between the two sets. Also a -ve value implies that the change made in the experiement is _bad_ (the bigger the number the wore the change).

The T-Statistic does assume a normal distribution of behaviour. There are alternatives like:

* **Fishers exact test** - for clickthrough rates
* **E-test** - for transactions per user
* **Chi-squared test** - for product quantities purcahsed

### The P-Value

Is the probability of A and B satisfying the _null hypotheses_.

This means that the experiement did **not** have any affect on the behaviour of your users. So as P-Value tends to 0 is better (implies significance) than a P-Value that approches 1 which is worse (implies there is no significance with the change.)

* **Low P-Value** - means there was an affect from the change (better)
* **High P-Value**- means there was very little to no affect from the change (worse)


Before running the experiment you might want to choose the threshold for the P-Value. Perhaps 1% or maybe 5%. Need to agree with the business area owners.

When the experiment is complete, measure the P-Value and if its less than the threshold agreed on then you can immediately reject teh null hypthesis and...

* If its a positive change, roll it out to Production!
* If its a negative change, discard the experiment immediately as its probably loosing the business money!

### Overview

What we ideally are looking for then is **a heigh T value and a low P value**.

## Example T-Value and P-Value

Open up Jupyter notebook [TTest](examples/TTest.ipynb) and have a play around!