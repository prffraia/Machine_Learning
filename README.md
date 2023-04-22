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

## Experimental Design

## Results

## Conclusions
