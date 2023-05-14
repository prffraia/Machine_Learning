# Machine Learning Project

## Title
Customer Segmentation Based on RFM Analysis

## Members: 
Giacomo Rossi - 763391

Flavia Martini - 766881

Fraia Pérez-Rayon - E13137 

## Introduction
The aim of this project is to predict the customer segmentation based on the RFM analysis. The RFM analysis is a measure of the frequency, recency and monetary of purchases of the same customer. 
The initial phase of our research involved performing an exploratory data analysis (EDA) with the objective of identifying the presence of missing values, duplicates and determining the distributions of the features. Subsequently, we utilized the RFM analysis method to predict the segmentation of customers based on their purchasing behavior. The RFM values, which were derived from the analysis, served as the basis for clustering the customers into distinct groups. The final stage of our analysis involved the application of clustering techniques to group the customers according to their RFM values. 


## Methods

### EDA
During the course of our research, we conducted an analysis of the feature distributions and observed that certain features, such as Customer City, Seller City, Customer State, and Seller State, exhibited a significant long tail. Given the need to transform these features into numeric values, we evaluated classical encoding techniques such as LabelEncoder and OneHotEncoder. However, these methods were deemed unsuitable due to issues such as incorrect encoding (LabelEncoder) and high computational costs (OneHotEncoder). To address this challenge, we opted to employ the TargetEncoder, a technique that encodes categorical values based on their frequency. The TargetEncoder was selected as the most appropriate method for encoding the aforementioned features, thereby enabling us to obtain more accurate and computationally efficient results. Our investigation revealed that several other variables, such as price, payment_value, and freight_value, also displayed long-tailed distributions, with the majority of the values concentrated near zero. Despite this characteristic, we determined that applying transformations to these variables would yield inconsistent results and, thus, decided not to employ any transformations.
We proceeded to encode the order_status, payment_type, and product_category_name_english columns using a classical label encoder. To address the datetime object variable, we utilized the timestamp method to convert the dates into numeric values. We observed that the dataset contained no missing values but had 83 duplicated entries, which we eliminated from the dataset.
Further analysis of the data revealed a high correlation of 76% between the price and payment_value variables. However, we chose not to remove these variables, despite their high correlation, as doing so would have resulted in a significant loss of valuable information. 


### Market Segmentation
As part of our data analysis, we created three new features to better understand customer behavior. 
The first feature, Recency, involved identifying the most recent purchase date by obtaining the maximum value of the purchase_date column. We then grouped the data by customer and determined their most recent purchase date by subtracting it from the maximum value of the purchase_date column.
For the second feature, Frequency, we computed the frequency of unique items per order for each customer. This was achieved by grouping the data by 'customer_unique_id' and then counting the number of unique values in the 'item_per_order' column for each group.
The third feature, Monetary, involved evaluating the monetary value of each customer's purchases. To accomplish this, we grouped the data by customer and calculated the sum of the payment values for each group.
The creation of these new features allowed us to gain insights into customer behavior by providing a more granular understanding of the recency, frequency, and monetary value of their purchases. 

### Clustering
As part of our study, we standardized the data using a Standard Scaler before applying clustering algorithms. We then utilized the K-Means algorithm to cluster the data into distinct groups.
To determine the optimal number of clusters for our data, we utilized both the elbow method and the KneeLocator algorithm. These methods allowed us to effectively visualize the variance explained by the different numbers of clusters, and select the optimal number of clusters based on the point of maximum curvature.


## Experimental Design
To accurately segment our customers, we compared the results obtained from both the K-Means and Hierarchical Clustering algorithms. We began by implementing the K-Means algorithm, which was found to be computationally efficient and required only a few seconds to train on our dataset.
In order to identify the optimal number of clusters for our data, we employed both the Scree Plot and the KneeLocator algorithm. These methods were chosen due to their speed and ease of interpretation, which is critical from a business perspective.
The optimal number of clusters was found to be 5, with each cluster exhibiting distinct distribution patterns. The resulting distribution of clusters can provide valuable insights for targeted marketing and business strategies:

Cluster 1: 6309

Cluster 0: 6229

Cluster 3: 986

Cluster 2: 162

Cluster 4: 32

Upon examining the cluster distribution obtained from the K-Means algorithm, we observed that two clusters had the highest number of observations, one cluster had a moderate amount, and the remaining two clusters had a relatively small number of observations. This clustering scheme appeared to be reasonable, as it aligned with our business objectives, as outlined in the Results and Business Implications section.

Next, the Hierarchical Clustering algorithm exhibited a higher computational cost compared to the K-Means algorithm. To determine the optimal number of clusters, we employed the Silhouette method. Although this method is more accurate than the Scree Plot, it is less intuitive.
Our analysis revealed that the optimal number of clusters using the Hierarchical Clustering algorithm was also 5, and the resulting cluster distribution is presented below:

Cluster 0: 8535

Cluster 2: 4543

Cluster 3: 411

Cluster 1: 201

Cluster 4: 28

The distributions of the clusters obtained from the K-Means and Hierarchical Clustering algorithms are notably dissimilar, with the latter showing one cluster containing the majority of observations, resulting to be the 65% of the total observations. After careful consideration, we decided to use the K-Means algorithm for its low computational cost, interpretability, and consistent results. The choice of algorithm was made after analyzing the distribution of the clusters and evaluating the advantages and drawbacks of each approach.


## Results
In order to visualize the distribution of the clusters in a three-dimensional space, we created a 3D plot. 

![image](https://github.com/giakomorssi/Machine_Learning/assets/115655415/435ce6ff-6be8-4e51-9967-5fb1044bf6d2)

Each cluster is represented by a different color, and the axes correspond to the RFM values of recency, frequency, and monetary. 
The plot shows that the clusters are clearly separated and have distinct ranges of RFM values. This visualization gives us a clear understanding of how the clusters are separated in the RFM space.

Regarding the business implication of the clustering results, we can identify the characteristics and behavior of each cluster to gain insights that can be used to tailor marketing strategies and improve customer experience. By understanding the different segments of customers, companies can allocate their resources more efficiently and effectively. 

The results are the following:

**•	Cluster 0: Purple**
This cluster has the highest monetary value, the 2rd highest recency value, it has the highest frequency, but it has only few observations (28).
It identifies the top customers. They are the customers that spemd the most , they have boght recently, and they have the most items for each order. The goal with them is to keep them as they are without losing them.

**•	Cluster 1: Orange**
This is the cluster with the most recent purchases, but is has the lowest monetary value and the lowest frequency. It is the cluster with the most observations.
This cluster identifies the new customers who have made only a few purchases at a relatively low price. Our goal here is to encourage them to increase their spending and make repeat purchases, thereby preventing them from falling into the previous cluster.

**•	Cluster 2: Blue**
This is the cluster with the highest recency value (longer time since last buy), and has the 2nd lowest monetary value and the 2nd lowest frequency. It is the 2nd cluster by size.
This cluster identifies a group of customers who haven't made a purchase in a long time. We can refer to them as "Lost Customers," and our objective is to re-engage with them and encourage them to make a purchase again.

**•	Cluster 3: Green**
This cluster has the 3nd lowest recency and has the 2nd highest monetary value. It has the 2nd highest frequency but it has few observations.
identifies a group of customers who have made recent purchases and tend to buy a high quantity of products per order while spending nearly as much as the Top Customer Cluster (Cluster 0). The goal for these customers is to increase their average spending to move them into the Top Customer Cluster.

**•	Cluster 4: Red**
This cluster has the 2nd highest recency, it has the 3rd highest monetary value and it has a medium frequency. It has a medium amount of observations.
It represents the average customer who has made recent purchases, buys a moderate amount of items per order, and spends a moderate amount of money. Our goal with this cluster is to encourage them to increase their spending and buy more items per order, with the aim of moving them towards the Top Customers cluster.

## Conclusions

Which cluster to target

## Appendix A: Code Description

### 01_EDA.ipynb

We provided the Notebook on the GitHub page with also the link to the colab notebook. The two files are slightly dfferent.
If you wish to run the one loaded in the GitHub page, you have to make sure the dataset is in the same directory

