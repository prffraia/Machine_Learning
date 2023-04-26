# Machine Learning Project

## Title
Customer Segmentation Based on RFM Analysis

## Members: 
Giacomo Rossi - 763391
Flavia Martini - 
Fraia

## Introduction
The aim of this project is to predict the customer segmentation based on the RFM analysis. The RFM analysis is a measure of the frequency, recency and monetary of purchases of the same customer.
We started with an Exploratory Data Analysis with the aim of vchecking the presence of null values, duplivates and check the distributions of the features. 
We then used the RFM analysis to predict the customer segmentation.
At the end we clustered the customers based on their RFM values obtained before.

## Methods

### EDA
We looked at the distributions of our features and the first thing we noticed was the unbalancness of the Customer City, Seller City, Customer State and Seller State.
We needed to transform them into numeric values but the classical encodings were either wrong (LabelEncoder) or needed to much computational costs (OneHotEncoder). We decided to use the LeaveOneOutEncoder which encodes the categories based on its frequency.
We transformed the order_status, payment_type, product_category_name_english columns with a classical label encoder.
To deal with the datetime object we used the timestamp method to transform them into numbers.

### Market Segmentation
We created 3 features:
- Recency: we found the most recent purchase date, we grouped by customer and evaluated the recency. 
- Frequency: we grouped by customer evalueted the frequency by checking the item per order of each customer
- Monetary: we grouped by customer and evaluated the monetary by summing the payment values.

### Clustering
We scaled the data with a Standard Scaler.
We used the K-Means algorithm and the Hierarchical Clustering algorithm.
The results were very similar but in terms of computational cost the K-Means algorithm was the best choice.
To choose the best number of clusters we used the elbow method and the KneeLocator algorithm.

## Experimental Design

## Results
The results are the following:
We identified 5 clusters.
* **Cluster 0: Blue**

  This cluster has the `highest monetary value`, the `2rd highest recency value`, it has the `highest frequency` but it has only `few observations (28)`.

* **Cluster 1: Orange** 

  This is the cluster with the `most recent purchases`, but is has the `lowest monetary value` and the `lowest frequency`. It is the cluster with `the most observations`.

* **Cluster 2: Green**

  This is the cluster with the `highest recency value (longer time since last buy)`, and has the `2nd lowest monetary value` and the `2nd lowest frequency`. It is the `2nd cluster by size`.

* **Cluster 3: Red**

  This cluster has the `3nd lowest recency` and has the `2nd highest monetary value`. It has the `2nd highest frequency` but it has `few observations`.

* **Cluster 4: Purple**

  This cluster has the `2nd highest recency`, it has the `3rd highest monetary value` and it has a `medium frequency`. It has `a medium amount of observations`.


## Conclusions

Decide how and which cluster to target.
