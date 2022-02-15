# movie_recommendation_system
* Over the last few years I have been using the IMDb app to track and rank the movies I'm watching. After collecting and rating more than 500 movies, I thought it would be interesting to use this data to recommend movies for me.
* In this notebook, I use MovieLens 20M Dataset and my own personal ranking to create a recommendtion engine (and recommend movies for myself:) )

#### Dataset

The MovieLens dataset was downloaded from Kaggle: https://www.kaggle.com/grouplens/movielens-20m-dataset?select=movie.csv

* MovieLens datasets describe ratings from MovieLens, a movie recommendation service. 
* It contains 20000263 ratings across 27278 movies. 
* These data were created by 138493 users between January 09, 1995 and March 31, 2015. 
* My personal ranking dataset was creating using imdb Watchlist feature


#### The Algorithm
* There are many different ways to build recommendation systems. Often, simple solutions and implementations result in the best results. In this notebook, I will demonstrate an intuitive algorithm based on singular value decomposition.
* We will predict a rating for a user-movie pair based on the ratings given by other users to the same film. 

Steps:
1. Create a sprase n by p user-rating matrix M with users as the index, movies as the columns and rating as values (0 is doesn't exists). Normalize the matrix such that every movie has a 0 mean rating.
2. Take the singular value decomposition of M = U Sigma V^T  where V is an orthogonal p
by p matrix (the columns of which are the eigenvectors of the covariance matrix of movies), U is an n by n  orthogonal matrix and Sigma is a (sorted) n by p dignoals matrix.
3. The columns of V are vectors in R^p representing weights for each film and are view as "factors" (or principal components)
4. We then take only k columns of $V$, $V_k$, and map each user ranknig row-vector M_i (rows of M) to: M_i to M_i V_k V^T_k, thereby projecting each user into a k-dimensional subspace.

<img width="1000" alt="data_map" src="https://github.com/hiladar0/movie_recommendation_system/blob/main/images/First%20principal%20component%20movie%20weight%20vs%20number%20of%20votes%20to%20the%20movie.png">
<img width="1000" alt="data_map" src="https://github.com/hiladar0/movie_recommendation_system/blob/main/images/First%20and%20second%20principal%20components.png">



#### Recommending movies for my self
Top rating prediction vs my actual rating:
<img width="1000" alt="data_map" src="https://github.com/hiladar0/movie_recommendation_system/blob/main/images/pred_vs_my_rating.png">
