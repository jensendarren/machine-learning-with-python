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