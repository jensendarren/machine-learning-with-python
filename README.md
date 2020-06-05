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

# Course Contents

1. [Python Basics](/1-Python-Basics/)
1. [Statistics Refresher](/2-Statistics-Refresher/)
1. [Predictive Models](/3-Predictive-Models/)
1. [Machine Learning](/4-Machine-Learning/)
1. [Recommender Systems](/5-Recommender-Systems/)
1. [Data Mining and Machine Learning](/6-Data-Mining-and-Machine-Learning/)
1. [Dealing with Real World Data](/7-Dealing-with-Real-World-Data/)
1. [Machine Learning On Big Data](/8-Machine-Learning-On-Big-Data/)
1. [Machine Learning In The Real World](/9-ML-In-The-Real-World/)

### Further Reading

* [Submitting a python job to Apache Spark on docker] https://medium.com/@thiagolcmelo/submitting-a-python-job-to-apache-spark-on-docker-b2bd19593a06
* [Unit tests in pyspark using pythons mock library]https://towardsdatascience.com/stop-mocking-me-unit-tests-in-pyspark-using-pythons-mock-library-a4b5cd019d7e