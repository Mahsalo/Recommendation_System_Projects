# Recommendation System

Recommendation systems are used to predict what items might a user be interested in. For example, it could tell us what movies a user might like based on his previous choices, or what rating would he give to a specific movie based on his previous ratings to similar movies. 

- Recommendation systems could be also used to suggest users for items which is called "targetting" in the marketting.
- Recommendation systems are used for the personalization of the users and items.


* In general, the item-user matrix or the **utility/feedback matrix** is a **sparse matrix** that needs to be filled with ratings.
* There are different methods to fill-out this sparse matrix: 
  1. Content Based Approach: In this method, we have the meta data about the content, for example we know that a specific user likes a specific group of items so we recommend her the most popular item in that group (based on properties of the items). This requires hand-engineering features.
  2. Collaborative Filtering: In this method we don't need a metadata and we just have the interactions matrix. Similar users like similar items. This method would have automatic feature engineering.
  
     * Model-Based method --> Matrix Factorization
     * Memory-Based method 
 
  3. Knowledge-based
  
  4. If we have both the interactions matrix and the metadata we can use the hybrid method by combining all 3 types of recommendation systems and use NNETs (Hybrid model like YouTube).    
     
* In matrix factorization method, the utility/feedback matrix would be estimated by the multiplication of two matrices corresponding to the items and users, separately. 
* The unknown values in the U and V matrices corresponding to the users and items, respectively, would be estimated by minimizing the distance between their multiplication with the feedback matrix.
* Optimizing the objective function could be done using:
  * SVD (Consider the feedback matrix factorized as the multiplication of users-factors and items-factors matrices). SVD would be minimizing the RMSE which is awesome BUT it sums in terms of ALL values but we have missing values!
  * SGD (Stochastic Gradient Descent), slower convergence compared to WALS
  * WALS (Weighted Alternating Least Square), this is the same as the SVD method but we are just summing over the known values so the distance between the multiplaction of two unknown matrices and the feedback matrix is computed only over the known values.

* **Important**: The rank in WALS shows the number of the factors/features that we want to find for user-factor and item-factor matrices. But we don't know this number so. we start with an initial value and then we can tune it for better predictions.
* In ALS, the optimization problem would be **iterative** and it would be alternating between:
  * Fixing the matrix U and solving for V
  * Fixing the matrix V and solving for U
  * In matrix factorization, at the training step we would like to find the number of characteristics that are the important features of the items in the recommendation part. At the test step, we already know the characteristics and would use that information to predict the rating for the unknown items and users (without prior information).
  * 
  
![ALS Formula](https://drive.google.com/file/d/1jGv9ZUD14e8dOYmjKcyrEog4Cu_EKXq6/view?usp=sharing?raw=true)

# Some Pitfalls:
1. Sparse rating matrix
2. Skewed rating matrix since some of the items might be more popular or some users just like/hate everything.
3. Maybe a new item is added and there is no info. about it.
4. Lack of explicit ratings about an item so we should rely on the implicit information/user feedback. 
5. Cold start problem: Visitor cold start and product cold start, It happens when there is a new visitor/user or a new product without any data.


# Recommender Systems Implementations: 
* Retailrocket recommender system dataset: I have designed a recommender system based on the "event.csv" file of this dataset which is collected from an ecommerce website. This file contains the behavior data of users of an ecommerce website. We have around 2.76 million items as well so our feedback matrix is of dimensions 2.7 m * 2.7 m. We would like to predict the future behavior of users for specific items based on their previous behaviors towards different items. These behaviors include: viewing the item, adding to cart and placing an order.
* I have used Pyspark (A Python API that supports Spark for the big data analysis) and implemented the recommneder algorithm on *Data Bricks* clusters.

https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/7194191126325765/1471038362177880/6285802778455178/latest.html

* Retailrocket dataset has 2,756,101 events including 2,664,312 views, 69,332 add-to-carts and 22,457 transactions produced by 1,407,580 unique visitors.
We have just used one of the datasets which is called "events.csv" and it has 5 columns: timestamp, visitor id, event, timeid and transaction id.

* The necessary steps towards solving recommender system problem are as following:

1. Data Wrangling and Pre-processing:  Since we have raw data lots of data wrangling and preprocessing is needed such as removing the unnecessary columns like timestamp, counting the number of the "views", "transactions" and "add-to-carts", casting the datatype to an appropriate one, removing the NaN and NULL values. The dataframes are also changed into RDD (Resilient Distributed Datasets) which is the default for the big data analysis in Spark since it makes the parallel computations faster.

2. Randomly splitting the dataset into training, validation and test (60%,20%,20%).

3. Defining the evaluation function that computes the RMSE for predicted and actual ratings.

4. Finding the best **rank** in the ALS algorithm. The rank shows the number of the latent/hidden factors and it depends on the data. The higher the value of rank the better the predictions BUT it might cause *overfitting* and it will consume more time and memory so finding the best rank is important. 
We can start with ranks 5-10 and then increase it to get a better performance. The best rank is 20 according to the limited computing resources (clusters) on free trail DataBricks account.

5. I have re-defined the *rating* for this problem in order to consider the behaviors of the users. In other words, if the user does not do anything about the item (not interested) the weight/rating is 1, if he just views the item the weight/rating is 2, if he adds the item to his cart the weight is 3 but if he buys the item the weight/rating is set to 5. 

