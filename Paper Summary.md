### Session 1: Paper Summary

Understanding the Explainable Cluster Analysis Framework
The two papers by Alvarez Garcia and colleagues (2024) explain how clustering can be used to discover meaningful patterns in complex datasets while making the results easier to understand. The first paper introduces a framework for explainable cluster analysis, while the second paper applies this approach to student data from PISA 2022.
The main idea is that clustering should not simply divide data into groups. It should also help researchers understand why those groups are different and what the results mean in real situations.

## 1. The Four Steps of the Framework

The framework consists of four main steps: data preprocessing, dimensionality reduction, clustering, and classification.
Data preprocessing is the first step. Real datasets often contain missing values, unusual observations, and variables measured on different scales. These problems can affect the accuracy of clustering. The first paper introduces several methods for handling missing values and uses Isolation Forest to identify outliers. This step helps improve data quality before analysis.
Dimensionality reduction is the second step. When a dataset contains too many variables, finding meaningful patterns becomes difficult. The researchers use Sparse Principal Component Analysis (SPCA) for numerical variables and Multiple Correspondence Analysis (MCA) for categorical variables. These methods reduce the number of dimensions while preserving useful information and improving interpretability.
Clustering is the third step. Its purpose is to group observations that share similar characteristics. The first paper compares methods such as K means, Gaussian Mixture Models, and Agglomerative Clustering. Different methods can produce different results, so evaluating cluster quality is important.
Classification is the final step. After clustering, the generated cluster labels are used as target variables for a supervised learning model. The model learns to predict cluster membership based on the original features. This helps researchers identify which variables are most important for distinguishing the groups.

## 2. Why Clustering Results Need Interpretation

Clustering is an unsupervised learning method, meaning that the algorithm groups observations without predefined labels. However, knowing that a dataset contains several clusters does not automatically explain what each cluster represents.
For example, if students are divided into seven groups, the group numbers alone do not tell us whether the students have different academic backgrounds, access to technology, or learning environments.
This is why interpretation is important. Researchers need to examine the characteristics of each cluster and identify the variables that make the groups different. Without interpretation, clustering results may be difficult to use for practical decisions.
The second paper demonstrates this using data from 30,800 Spanish students. The researchers reduced 74 original variables to 16 derived variables and identified seven student clusters. Their analysis showed that socioeconomic status and access to and use of information and communication technology were important factors in distinguishing student profiles.
These findings show how clustering can provide useful information when the results are properly explained.

## 3. How Classification Helps Explain Clusters

Classification helps researchers understand clustering results by treating the generated cluster labels as the target variable.
After clustering is completed, a classification model is trained to predict which cluster each observation belongs to. The model can then be analyzed to determine which original features contribute most to those predictions.
The papers introduce tree based classification models and SHAP values as tools for interpretation. SHAP helps explain how individual variables influence a model's predictions. Global SHAP values show which variables are important across the dataset, while local SHAP values help explain the characteristics of particular observations or clusters.
In the PISA 2022 study, the researchers used an XGBoost classifier and achieved an accuracy of 86.43 percent. They then used SHAP values to understand the factors that distinguished the seven student groups.
This shows that classification is useful not only for predicting cluster membership but also for explaining the patterns discovered through clustering.

## 4. Connection to Our Final Project

Our team plans to apply this framework to Seoul Public Bicycle rental data. We want to identify different bicycle rental patterns and understand which factors distinguish them.
We will first prepare the dataset by checking missing values, outliers, and variable types. Next, we will apply dimensionality reduction to simplify the data. We will then use clustering to identify groups with similar rental patterns.
Finally, we plan to train a classification model using the cluster labels and examine feature importance to explain the differences between groups.
By following this framework, our goal is not only to identify rental patterns but also to understand what makes each pattern different. This could provide useful insights into bicycle usage and help support decisions about public bicycle services.

## Conclusion

After reading both papers, I understood that clustering becomes more useful when the results can be clearly explained. Data preprocessing and dimensionality reduction help improve the quality of the analysis, while clustering identifies patterns and classification helps explain them.
The most important lesson is that finding groups is only part of the analysis. Understanding the characteristics of those groups is what makes the results meaningful and useful for decision making.
