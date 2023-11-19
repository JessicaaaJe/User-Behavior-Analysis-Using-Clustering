# Clustering---user behavior analysis

### DataSet:
This study is mainly focused on using a churn-risk dataset: https://www.kaggle.com/datasets/undersc0re/predict-the-churn-risk-rate/


This dataset contains 36992 user observations with 23 variables focusing on users' behaviors toward one product:
age, gender, security number, region category, membership, 
joining date, joined through referral, referral ID, preferred offer types, medium of operation, internet option, last_visit_time, 
days_since_last_login, average time spent, average transaction value, average A large amount of missing values needs to be handled. 

To test around the function we write, In Part A, we use a different simple data set for e-commerce.
E-commerce: There are in total 500 observations and 6 columns in this dataset, except for the first column, which is a number indicator. The dataset contains five continuous features: Average Session Length, Time on App, Time on Website, Length of Membership, and Yearly Amount Spent 


### Study Objective:

1: We are interested in finding out whether members of different memberships could be grouped by given features or a subset of them. There are six classes of memberships: no membership, basic membership, silver membership, gold membership, platinum membership, and premium membership. 
2: Discover the characteristics of each cluster to gain insights into customer behaviors to facilitate the company’s further actions to improve the marketing or promotion strategy. 

### Code Structure:
Data Cleaning 
Model Fitting: 
Testing the best hyperparameters for K-means
Testing the best hyperparameters for hierarchical clustering
Testing the best hyperparameters for DBSCAN
Model Evaluation
discussion on the two work objectives 

### Evaluation: 
After fitting three types of models: KMeans, DBSCAN, and hierarchical, and find the optimal hyperparameters for each algorithm. 
silhouette score is used to compare their performance. 
And here is the silhouette score for three models: 

Kmeans Silhouette Score: 0.89
hierarchical Silhouette Score: 0.89
DBSCAN Silhouette Score: 0.99

All three are well performed; we will choose the one with the highest value, DBSCAN, to study the two objectives of this work. 

For the first objective, I did a membership's purity check on each cluster to see how membership is distributed across clusters. Overall, the purity performance is decent, given that we have six classes in'membership_category'. If we do a random guess, the purity will be around 0.167. Achieving a purity of 0.4 means that the dominant class in a given cluster makes up 40% of the cluster's data points. This is significantly better than the 16.67% you'd expect from a random assignment. It shows that the clustering algorithm is picking up some structure in the data related to the classes.

But considering that'membership' does not have to be the primary customer segmentation factor, I would like to take a deeper look at some interested features of each cluster to see the possible implications, which matches our second objective
By printing out the membership distribution within each cluster, we can see that cluster 0/3/6/8/10/12 has a high number of Premium and Platinum membership users, which indicates that these clusters contain the most loyal or high-value customers.
And clusters 1/ 2/ 7/ 9 has users mostly centered in the 'no membership' and 'basic membership' categories.  We will take a look at other features of these two groups of clusters to see how user behaviors are related to memberships.

We will put those interesting features into three categories: 1. demographics; 2. user engagement; and 3. churn risk. 

Specifically, we look at the age and gender variations in the demographic section, and, surprising enough, both do not show a big difference between groups. The average age in the high-loyalty user groups is similar to the age in the low-loyalty groups. And the spread of gender is almost half in each cluster. 
And for user engagement, we specifically look at the variables ‘points in wallet’ and transaction value. The difference in these two variables between groups is obvious. The average number of points in wallets in high loyalty user clusters is around 50, while in low loyalty user clusters, the value is around 36. The average transaction value in high-loyalty user clusters is around 35000, while in low-loyalty user clusters, the value is around 25000. 

Finally, we look at the churn risk score. Within the high loyalty clusters, the probability of having no churn risk is 100%, which is much larger than the probability across all data 
points, which has a probability of 45.89%. In all low-loyalty clusters, the probability of having a churn risk is 100%. The reason for this kind of extreme statistic might be that the churn_risk_score is a fitted feature in the clustering process. 

To conclude, we could see that high-loyalty users usually have more points in their wallet, a higher transaction value, and a low probability of having churn risk, and vice versa for low-loyalty users. Based on those clusters, the company can create personalized marketing campaigns to target each group based on their behavior. For the high-loyalty group, they can focus on retention strategies and cross-selling or up-selling higher-value products. For the low-loyalty group, strategies could focus on increasing engagement and trust. 

### Further Discussion
I also did an evaluation of the promotion strategy the company had, including special discounts and preferred offer types. When we check the percentage use of the special discount, the data shows that the use rate is relatively similar across high loyalty users and low loyalty users. It suggests that the discount strategy is not effectively differentiated to cater to the distinct needs or preferences of these two groups. The company may need to consider other effective approaches, specifically targeted at low-loyalty groups, to boost sales and reduce churn risk.  And compared with credit or debit card offers, high loyalty groups are more willing to be offered gift vouchers or coupons. So the company may think of this as a hint to improve their strategy.
Limitation
Although there are a large number of variables, most of them do not give a good performance result in clustering. So only a small number of variables are included in the model, which might result in bias and limitations to the interpretation of user’s behaviors. 
A more complete dataset that includes more user behavior features might be helpful. 
