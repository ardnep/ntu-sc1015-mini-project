# SC1015: Data Science Mini Project - Unconventionality & Success

School of Computer Science and Engineering \
Nanyang Technological University \
Lab: SC14 \
Group : 6 

Members: 
1. Bernice Koh Jun Yan ([@bernicekjy](https://github.com/bernicekjy))
2. Nepal Aaradh ([@ardnep](https://github.com/ardnep))
3. Veeraraghavan Srivathsan Nithyasri ([@Veeraraghavan-S-Nithyasri](https://github.com/Veeraraghavan-S-Nithyasri))

---
### Description:
This repository contains all the Jupyter Notebooks, datasets, images, video presentations, and the source materials/references we have used and created as part of the Mini Project for SC1015: Introduction to Data Science and AI. 

This README briefly highlights what we have accomplished in this project. If you want a more detailed explanation of things, please refer to the the Jupyter Notebooks in this repository. They contain more in-depth descriptions and smaller details which are not mentioned here in the README. For convenience, we have divided the notebooks into 5 parts which broadly relate to the 5 main sections of this project.

---
### Table of Contents:
1. [Problem Formulation](#1-Problem-Formlation)
2. [Data Preparation and Cleaning](#2-Data-Preparation-and-Cleaning)
3. [Exploratory Data Analysis](#3-Exploratory-Data-Analysis)
4. [Dimensionality Reduction](#4-Dimensionality-Reduction)
5. [Clustering](#5-Clustering)
6. [Data Driven Insights and Conclusion](#6-Data-Driven-Insights-and-Conclusion)
7. [References](#7-References)
---
### 1. [Problem Formulation](https://github.com/ardnep/ntu-sc1015-mini-project/blob/a1e85b5ec7fdeeaca5ddf6c4cdc55a9e95874124/Part_1_Data_Prep_Cleaning.ipynb)

**Our Dataset:** [Stack Overflow Developer Survey 2020 on Kaggle](https://www.kaggle.com/aitzaz/stack-overflow-developer-survey-2020) \
**Our Question:** Does Being Unconventional Determine Success? 

**Success:** Determined using Salary and Job Satisfaction \
**Unconventional Individuals:** Outliers/anomalies found after clustering individuals based on the  technologies they use such as Web frameworks, Programming languages, Operating systems, etc.

**Rationale:** We believe that this dataset as well as the question we pose is very relevant to the SCSE community at NTU. Being students of SCSE, once we graduate, we might become developers ourselves. By learning what kinds of developers tend to be more successful, we might be able to understand what it takes to be successful in the software development world. 

### 2. [Data Preparation and Cleaning](https://github.com/ardnep/ntu-sc1015-mini-project/blob/a1e85b5ec7fdeeaca5ddf6c4cdc55a9e95874124/Part_1_Data_Prep_Cleaning.ipynb)
In this section of the project, we prepped and cleaned the dataset to help us analyze our data better and also to help us use our data for the purposes of machine learning in the later sections. 

We performed the following:
1. **Preliminary Feature Selection:** `8` relevant variables out of `61` were selected.
2. **Dropping `NaN`s**: All the `NaN` values in these `8` variables were dropped. 
3. **Splitting Dataset in Two:** The `8` variables were then split in 2 DataFrames. One with `6` variables relating to conventionality and the other with `2` relating to success. 
4. **Encoding Categorical Variables:** The categorical variables in both the DataFrames were encoded appropriately. 

### 3. [Exploratory Data Analysis](https://github.com/ardnep/ntu-sc1015-mini-project/blob/e79194b4337bb109729f915ef474e608031fd4f8/Part_2_EDA.ipynb)
Then, we explored each of our two DataFrames further using Exploratory Data Analysis to answer questions like are there any patterns we are noticing? What do our success variables look like? What about the conventionality variables? Are there any underlying relationships between them? Can we make any inferences for our question at this stage? 

To achieve this we did the following:
1. **Explored `ConvertedComp`**: This variable is the annual compensation in USD (a.k.a Salary). Median of around $54k was seen. A lot of outliers with high salaries were present.
2. **Explored `JobSat`:** This variable is the job satisfaction (`0-4` scale). Most frequent ratings were `2` and `4`. The mean rating was at `2.3`.
3. **Explored Relationships Between `JobSat` and `ConvertedComp`:** Weak correlation was seen between `JobSat` and `ConvertedComp`.
4. **Explored Variables Related to Conventionality:** Studied which options in the `6` variables were more frequently selected by respondents. 

For further findings and explanations, please refer to the Jupyter Notebook on EDA.

### 4. [Dimensionality Reduction](https://github.com/ardnep/ntu-sc1015-mini-project/blob/a1e85b5ec7fdeeaca5ddf6c4cdc55a9e95874124/Part_3_Dimension_Reduction.ipynb)
Our DataFrame with `6` variables after encoding was converted to a DataFrame  with `94` which is a very high dimensional data. 

This meant a few problems (curse of dimensionality):
1. It would probably not result in nicely formulated clusters.
2. High dimensional data is difficult to work with because of space and time increases when running algorithms on them.
3. High dimensional data is difficult to visualize.

So, **Multiple Correspondence Analysis (MCA)** was used to reduce these dimensions. The reason we chose MCA was that the general convention with dimensionality reduction is Principal Component Analysis (PCA), however it does not work well with categorical data which is what we have. MCA works well with multiple columns of categorical data. 

Using MCA, the dimensions were reduced from `94` columns to just `42`!


### 5. [Clustering](https://github.com/ardnep/ntu-sc1015-mini-project/blob/a1e85b5ec7fdeeaca5ddf6c4cdc55a9e95874124/Part_4_Clustering.ipynb)

With these `42` columns, we then performed clustering. We chose the **Hierarchical Density-Based Spatial Clustering of Applications with Noise (HDBCAN)**. 

The reasons for this are:
1. This is a density based clustering algorithm which means it does not need the specification of the number of clusters. Essentially, this algorithm will not *force* any point into a cluster. Instead, points which do not really belong to any cluster are labeled "noise". This is clearly useful for us since we are doing anomaly detection (outlier/noise detection).
2. Because this is density based, the shape of our data does not matter which is useful since we are working with high dimensional data and it is not possible for us to visualize and understand what kind of shapes our data might have. 
3. With a non-hierarchical DBSCAN, there are certain hyperparameters that are difficult to tune. HDBSCAN removes the need to tune some of these parameters. 
4. Because HDBSCAN is a hierarchical clustering algorithm even if we have a high dimensional data, we can use dendrograms to somewhat visualize the clusters and make inferences.

More details on HDBSCAN and its parameters are presented in the Jupyter Notebook on Clustering.

In this section, we performed the following:
1. Clustering with Random Parameters
2. Hyperparameter Tuning with GridSearchCV using DBCV Score
3. Clustering with New Parameters

Our final clustering resulted in a total of `3` clusters and `6206` outliers (out of `19362` total points).

### 6. [Data Driven Insights and Conclusion](https://github.com/ardnep/ntu-sc1015-mini-project/blob/e79194b4337bb109729f915ef474e608031fd4f8/Part_5_Data_Driven_Insights.ipynb)
Here, we re-combined our variables related to success and the clustered variables related to conventionality to see if there are any differences between outliers and non-outliers. We performed a comparative Exploratory Data Analysis on the outliers vs. non-outliers to see if we can infer anything from the similarities and differences. 

In this section, we also looked at the characteristics of the individuals in our `3` clusters using the variables related to conventionality. The findings have been presented in the Jupyter Notebook on Data Driven Insights. 

Most notably, however, we found that there were no difference in the distribution of the Salary or the Job Satisfaction among Outliers and Non-outliers (Conventional individuals and non-conventional individuals). So, we concluded that unconventionality might NOT be an indicator of success. 

### 7. References
1. [https://bookdown.org/brian_nguyen0305/Multivariate_Statistical_Analysis_with_R/what-is-mca.html](https://bookdown.org/brian_nguyen0305/Multivariate_Statistical_Analysis_with_R/what-is-mca.html) 
2. [https://pca4ds.github.io/mechanics.html](https://pca4ds.github.io/mechanics.html) 
3. [https://support.minitab.com/en-us/minitab/18/help-and-how-to/modeling-statistics/multivariate/how-to/multiple-correspondence-analysis/interpret-the-results/all-statistics-and-graphs/](https://support.minitab.com/en-us/minitab/18/help-and-how-to/modeling-statistics/multivariate/how-to/multiple-correspondence-analysis/interpret-the-results/all-statistics-and-graphs/)
4. [https://github.com/MaxHalford/prince](https://github.com/MaxHalford/prince)
5. [https://www.researchgate.net/post/What-should-the-minumum-explained-variance-be-to-be-acceptable-in-factor-analysis](https://www.researchgate.net/post/What-should-the-minumum-explained-variance-be-to-be-acceptable-in-factor-analysis)
6. [https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html](https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html)
7. [https://www.dbs.ifi.lmu.de/~zimek/publications/SDM2014/DBCV.pdf](https://www.dbs.ifi.lmu.de/~zimek/publications/SDM2014/DBCV.pdf)
8. [https://github.com/christopherjenness/DBCV](https://github.com/christopherjenness/DBCV)
9. [https://www.kdnuggets.com/2020/04/dbscan-clustering-algorithm-machine-learning.html](https://www.kdnuggets.com/2020/04/dbscan-clustering-algorithm-machine-learning.html)
10. [https://www.youtube.com/watch?v=dGsxd67IFiU](https://www.youtube.com/watch?v=dGsxd67IFiU)

