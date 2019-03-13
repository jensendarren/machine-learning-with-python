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