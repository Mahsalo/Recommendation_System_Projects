# Recommendation System

Recommendation systems are used to predict what items might a user be interested in. For example, it could tell us what movies a user might like based on his previous choices, or what rating would he give to a specific movie based on his previous ratings to similar movies. 

- Recommendation systems could be also used to suggest ussers for items which is called "targetting" in the marketting.
- Recommendation systems are use for the personalization of the users and items.


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
  * SVD
  * SGD (Stochastic Gradient Descent), slower convergence compared to WALS
  * WALS (Weighted Alternating Least Square)
* In ALS, the optimization problem would be **iterative** and it would be alternating between:
  * Fixing the matrix U and solving for V
  * Fixing the matrix V and solving for U
  
![ALS Formula](https://drive.google.com/file/d/1jGv9ZUD14e8dOYmjKcyrEog4Cu_EKXq6/view?usp=sharing?raw=true)

# Some Pitfalls:
1. Sparse rating matrix
2. Skewed rating matrix since some of the items might be more popular or some users just like/hate everything.
3. Maybe a new item is added and there is no info. about it.
4. Lack of explicit ratings about an item so we should rely on the implicit information/user feedback. 
5. Cold start problem:


