A comparison of recommender systems on a dataset with 20 million observations.

# Data

The data is from the [MovieLens 20M Dataset](https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset):

- 20 million observations
- 138k users
- 27k items (movies)

# Models

This is the current list. More models may be added later.

## PyTorch

A deep learning model built in PyTorch, using `Embedding()` layers for the inputs (user IDs, movie IDs), and a stack of `Linear()` (fully-connected) layers to evaluate the embeddings.

## Spark

Matrix factorization model via `ALS()`. Implemented in PySpark. By tuning the parallelism of the Spark context, the model can be trained on a single 64 GB RAM machine, although a cluster seems more appropriate at this size.

# Hyperparameter optimization

All models are optimized via Optuna. The hyperparameters that were optimized:

PyTorch: size of each layer, activation function, learning rate, momentum.

Spark: rank (number of latent factors), lambda (regularization strength).

The metric used for optimization was MSE on the test data.

# Results

The MSE values from the best models:

PyTorch: 0.0387

Spark: 0.0261

When making recommendations, there is broad agreement between models on the kinds of movies (genres) that are recommended. But there is very little overlap in terms of actual titles.

Since Spark has a substantially better MSE value, its predictions are likely more useful in practice on this dataset.

# TODO

Only user IDs, movie IDs, and ratings were used to make predictions. The dataset contains extra data about users and movies. More complex models may be able to use the extra data to make better predictions.
