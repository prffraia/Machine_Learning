# Machine Learning Project

## Title
Customer Segmentation Based on RFM Analysis

## Members: 
Giacomo Rossi - 763391

Flavia Martini - 766881

Fraia Pérez-Rayon - E13137 

## Introduction
The aim of this project is to predict the customer segmentation based on the RFM analysis. The RFM analysis is a measure of the frequency, recency and monetary of purchases of the same customer.
We started with an Exploratory Data Analysis with the aim of checking the presence of null values, duplicates and check the distributions of the features. 
We then used the RFM analysis to predict the customer segmentation.
At the end we clustered the customers based on their RFM values obtained before.

## Methods

### EDA

We looked at the distributions of our features and the first thing we noticed was that Customer City, Seller City, Customer State and Seller State had a very long tail.
We needed to transform them into numeric values but the classical encodings were either wrong (LabelEncoder) or needed to much computational costs (OneHotEncoder). We decided to use the TargetEncoder which encodes the categories based on its frequency.
Also other variables such as price, payment_value and fright_value had a long tail and the majority of the value were close to zero.
We decided to not apply any transformations, since the results were very different.
We then transformed the order_status, payment_type, product_category_name_english columns with a classical label encoder.
To deal with the datetime object we used the timestamp method to transform them into numbers.
The dataset had no null values, but had 83 duplicated that we removed.
Only the price and the payment_value had a high correlation of 76% but we decided not to remove any of the variables.

### Market Segmentation
We created 3 features:
- Recency: we found the most recent purchase date as the maximum of the purchase_date column. We then grouped by customer and found the most recenct purchase date and subtracted it from the maximum of the purchase_date column.  
- Frequency: We calculated the frequency of unique items per order for each customer. This was done by grouping the data by 'customer_unique_id' and then counting the number of unique values in the 'item_per_order' column for each group.
- Monetary: we grouped by customer and evaluated the monetary value by summing up the payment values.

### Clustering
We scaled the data with a Standard Scaler.
We used the K-Means algorithm and the Hierarchical Clustering algorithm.
The results were very similar but in terms of computational cost the K-Means algorithm was the best choice.
To choose the best number of clusters we used the elbow method and the KneeLocator algorithm.

## Experimental Design
To segment the customer in the best way possible we tried both the K-Means algorithm and the Hierarchical Clustering algorithm.
We started with the K-Means algorithm that took just few second to train. To find the optimal number of clusters we decided to use the Scree Plot and the KneeLocator algorithm. These methods combined are both fast and intuitive from a business point of view.
The optimal number of cluster turned out to be 5 and the distribution of the clusters are the following:
- 1: 6309
- 0: 6229
- 3: 986
- 2: 162
- 4: 32

As we can see we have 2 clusters that have the highest number of observations, one cluster with a moderate amount, and 2 cluster with few observations. This division is reasonable as we will see in the Results and Business Implication.
Following with the Hierarchical Clustering algorithm, the first thing we noticed was the high computational cost compared to the K-Means algorithm.
Moreover, to select the optimal number of cluster, we used instead the Silhouette method. This method is more accurate than the Scree Plot but is less intuitive. 
The number of clustrers turned out to be 5 as well with the following distribution:
- 0: 8535
- 2: 4543
- 3: 411
- 1: 201
- 4: 28

The distributions are very different from one another. 
The Hierarchical Clustering has one cluster containing 65% of the observations.
To conclude, we decided to use the K-Means algorithm for its low computational cost, interpretability and results. 

## Results
Moving to the results of the clustering, we can show a 3D plot of the clusters to see their distribution.

![image](https://github.com/giakomorssi/Machine_Learning/assets/115655415/a034a143-020c-4dea-8584-ca247424bb64)

From the plot we can see that the cluster are well separated.ù
Moving to the Business implication, we can also identify the meaning of each cluster so we can understand the customers and be able to target them accordingly.

The results are the following:

* **Cluster 0: Purple**

  This cluster has the `highest monetary value`, the `2rd highest recency value`, it has the `highest frequency` but it has only `few observations (28)`.

* **Cluster 1: Orange** 

  This is the cluster with the `most recent purchases`, but is has the `lowest monetary value` and the `lowest frequency`. It is the cluster with `the most observations`.

* **Cluster 2: Blue**

  This is the cluster with the `highest recency value (longer time since last buy)`, and has the `2nd lowest monetary value` and the `2nd lowest frequency`. It is the `2nd cluster by size`.

* **Cluster 3: Green**

  This cluster has the `3nd lowest recency` and has the `2nd highest monetary value`. It has the `2nd highest frequency` but it has `few observations`.

* **Cluster 4: Red**

  This cluster has the `2nd highest recency`, it has the `3rd highest monetary value` and it has a `medium frequency`. It has `a medium amount of observations`.

**Cluster 0 (purple cluster)** identifies the top customers. They are the customers that spemd the most , they have boght recently, and they have the most items for each order. The goal with them is to keep them as they are without losing them.

**Cluster 1 (orange cluster)** identifies the new customers, those that have just bought few products at a low price. Our goal here is to make them spend more and try to make them buy again, avoiding to make them follow in the previous Cluster.

**Cluster 2 (blue cluster)** indentifies that group of customer that haven't bought for a long time. So we can identify them as the 'Lost Customers' and our goal is to make tham buy again. 

**Cluster 3 (green cluster)** identifies that group of customers that have bought recently and that buy an high amount of products per order and that spend almost as the Cluster 0. The goal for these customer is to raise average receipt so that they fall into the Top Curtomer Cluster.

**Cluster 4 (red cluster)** identifies the average customer, that have bought recently, a moderate amout of items per order and they spent a moderate amount of money. 





## Conclusions


