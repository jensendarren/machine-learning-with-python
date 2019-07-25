### Recommender Systems

#### User-Based collaborative filtering

Based on your behaviour, interests, browsing and purchasing history as well as the actions of others - this system approach can be used to recommend products to the user.

* Build a matrix of things (basically a database table of users where the columns represent the item in question) that each user bought/viweed/rated. Maybe the schema is *User(id, category, product, rated?, purchased?, viewed?)*.
* Then, compute similarity scores between each user.
* Find users similar to you (or the person logged in).
* Recomend the things that the users similar to you bought/viweed/rated etc.

#### Problems with using user based collaborative filtering (CF)

It mostly boils down to the challenges of dealing with human nature, namely:

* People are fickle - their ideas and tastes change
* There are many more people than things. This basically means that focusing computational resources of recommending for Users is challenging since there are 7B people on the planet now, but not 7B movies, or music albums. So by that rational its better to focus on the similarities between products rather than users.
* People can do nasty things - basically meaning that people will always try to game the system.

#### Item-Based collaborative filtering

This means we are comparing items with one another - not people anymore. This solves a few issues like:

* A movie is always going to be the same movie - it does not change, its not fickle!
* There are fewer things than people (so less computation required)
* Its much harder to game the system.

The way this works is:

* Find every movie (or other) pairing that is watched by the same person.
* Measure the similarity of the ratings accross all users who watched both
* Sort by the movie and then similarity strength

So for example, take two films e.g. Star Wars and Empire Strikes Back, find people who watched both of these films, compare the rating that these people gave these films and if they are very similar then the movies must also be similar (in this example category).

There are other ways to do this, of course.

### Example using the Movielense data

Open up the [Similar Movies Examples](/examples/SimilarMovies.ipynb) notebook and explore in there. Many useful tips and usage examples of the [Pandas](https://pandas.pydata.org/) library!

Finally, checkout the [Item Based CF](/examples/ItemBasedCF.ipynb) notebook and explore in there. In this example, you will discover even more amazing power of Pandas! For example, Pandas has a built-in `corr()` method that will compute a correlation score for every column pair in the matrix! This gives us a correlation score between every pair of movies.