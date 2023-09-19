**Name: Hoda Shoghi**

**Contact: hoda.shoghi@gmail.com**

**Date: 05 Sep 2023**


# Introduction

### Project Title: 

# Predicting Restaurant Ratings: A Data-Driven Approach

# Goal

My goal is to build a predictive model that can accurately predict a restaurant's star rating by leveraging the vast amount of information in the dataset. This model can provide prospective Steakholders with insights into how certain factors might influence their new establishment's ratings.

# Dataset-Overview
The Yelp dataset offers a wealth of information about businesses across several cities. This project focuses specifically on restaurant businesses. The dataset includes attributes such as business ID, name, location, review count, categories, and star ratings.

You can dowload this dataset at https://www.yelp.com/dataset

| COLUMN NAME  | DESCRIPTION                                                    | DATA TYPE |
|--------------|----------------------------------------------------------------|-----------|
| business_id  | Unique identifier for the business                             | string    |
| name         | Name of the business                                           | string    |
| address      | Address where the business is located                          | string    |
| city         | City where the business is located                             | string    |
| state        | State where the business is located                            | string    |
| postal_code  | postal_code where the business is located                      | string    |
| latitude     | Geographical latitude of the business                          | float64   |
| longitude    | Geographical longitude of the business                         | float64   |
| stars        | Star rating of the business                                    | float64   |
| review_count |  Number of reviews the business has received                   | int64     |
| is_open      | 0 is closed and 1 is open                                      | int64     |
| attributes   | Dict-different attribute like payment method,  , etc | string  |
| categories   | Categories the business falls under                            | string    |
| hours        | Dict-Hours of operation                                        | string    |


#### Data Notes :
1- Yelp's dataset covers various types of businesses. For this project, I focus on businesses categorized as "Restaurants".

2- The `categories` column can contain multiple categories for a single business. For example, a restaurant can be categorized as both 'Italian' and 'Pizza'.

3- Yelp users rate businesses on a scale of 1 to 5 stars. This serves as our target variable, which we aim to predict with our model.

4- `attribute` Column contains dictionary of different attributes and their values

5- There are some nested dictionaries inside `attributes` Column like `Ambience` or `Business Parking`


## Table of Contents

1. [**Introduction**](#Introduction)
    * [Dataset Overview](#Dataset-Overview)
    * [Goal](#Goal)
2. [**Basic Data Wrangling**](#Basic-Data-Wrangling)
    * [Dataset Shape](#Dataset-Shape)
    * [Data Types & Distribution](#Data-Types-&-Distribution)
    * [Duplicates & Redundancy](#Duplicates-&-Redundancy)
    * [Null Value Handling](#Null-Value-Handling)
    * [Feature Removal](#Feature-Removal)
        * ["is_open" Column](#is_open-Column)
        * ["state" Column](#state-Column)
    * [Target Variable Analysis](#Target-Variable-Analysis)
        * [Descriptive Statistics for "stars"](#Descriptive-Statistics-for-stars)
        * [Transforming the "stars" column into a binary variable](#Transforming-stars)
    * [Missing Values in "categories" and "attributes"](#Missing-Values)
    * ["categories" Column Processing](#categories-Column-Processing)
        * [Standardization](#Standardization)
        * [Filtering for restaurants](#Filtering-for-restaurants)
        * [Category Flattening](#Category-Flattening)
        * [One-Hot Encoding](#One-Hot-Encoding)
        * [Handling Low-Count Categories](#Handling-Low-Count-Categories)
    * [Correlation Analysis](#Correlation-Analysis)
        * [Identifying Highly Correlated Variable Pairs](#Identifying-Highly-Correlated)
        * [Handling Highly Correlated Variables](#Handling-Highly-Correlated-Variables)
4. [**Attribute Column Analysis**](#Attribute-Column-Analysis)

5. [Checking for Duplicate Information](#Duplicate-Information)
    . [Finding Redundant Columns](#Finding-Redundant-Columns)
6. [Data Conversion](#Converting-binary-columns-to-uint8)

7. [Correlation Analysis](#Correlation-Analysis)
8. [Saving cleaned data to csv](#Saving-the-cleaned-data)
MODELING :
9. [Logistic Regression](#logistic-regression)
    - [RandomizedSearchCV](#logistic-regression)
    - [GridSearchCV](#GridSearchCV) 
    - [Logistic Regression-L2](#Logistic-regression-L2)
    - [Cross-Validation](#Cross-Validation)
    - [Classification Report](#ClassificationReport)
    - [Confusion Matrix](#Confusion-Matrix)
    - [ROC](#ROC)
    - [Precision-Recall Curve](#Precision-Recall-Curve)
    - [Feature Coefficients](#Feature-Coefficients)

10. [Random Forest](#Random-forest) 
    - [Random Forest Classification report](#Random-Forest-Classification-report) 

    - [Feature_importances & Model Refinement with Random Forest](#Feature_importances-&-Model-Refinement-with-Random-Forest) 
11. [Gradient Boosting (GBM)](#Gradient-boosting-gbm)
    - [PipeLine for  GradientBoostingClassifier](#PipeLine-for-GradientBoostingClassifier)
12. [XGBoost](#Xgboost) 
    - [PipeLine for XGboost](#PipeLine-for-XGboost) 
    - [XGboost Confusion_matrix](#XGboost-Confusion_matrix)
    - [Feature Mean Differences Analysis](#Feature-Mean-Differences-Analysis)
    - [SHAP Analysis for XGBoost](#SHAP-Analysis-for-XGBoost)
13. [Conclusion](#Conclusion)

 



