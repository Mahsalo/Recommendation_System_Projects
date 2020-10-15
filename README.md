# Recommendation System

Recommendation systems are used to predict what items might a user be interested in. For example, it could tell us what movies a user might like based on his previous choices, or what rating would he give to a specific movie based on his previous ratings to similar movies. 

* In general, the item-user matrix or the **utility/feedback matrix** is a sparse matrix that needs to be filled with ratings.
* There are different methods to fill-out this sparse matrix: 
  1. Content Based Approach
  2. Collaborative Filtering
  
     * Model-Based method --> Matrix Factorization
     * Memory-Based method 
     * Hybrid
     
* In matrix factorization method, the utility/feedback matrix would be estimated by the multiplication of two matrices corresponding to the items and users, separately. 
* The unknown values in the U and V matrices corresponding to the users and items, respectively, would be estimated by minimizing the distance between their multiplication with the feedback matrix.
* Optimizing the objective function could be done using:
  * SVD
  * SGD (Stochastic Gradient Descent), slower convergence compared to WALS
  * WALS (Weighted Alternating Least Square)
* In ALS, the optimization problem would be **iterative** and it wouold be alternating between:
  * Fixing the matrix U and solving for V
  * Fixing the matrix V and solving for U
  
![ddd](https://drive.google.com/file/d/1jGv9ZUD14e8dOYmjKcyrEog4Cu_EKXq6/view?usp=sharing)

# Recommender Systems Implementations: 

https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/7194191126325765/1471038362177880/6285802778455178/latest.html





