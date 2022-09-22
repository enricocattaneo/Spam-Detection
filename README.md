# Spam Detection

**OBJECTIVE**: Explore text message data and detect if a message is either spam or not by using different classification algorithms (Multinomial Naive Bayes, Support Vector Machine, and Logistic Regression).

## Table of Contents

- [Data Description](#datadescription)
- [Data Preparation](#datapreparation)
- [Classification Models](#classificationmodels)
- [Results](#results)


<a id='datadescription'></a>
## Data Description

Dataset **spam.csv**:

* **Number of Observations**: 5572

* **Number of Attributes**: 2 features. Target variable (binary: ham and spam), and messages' text variable (text)

<a id='datapreparation'></a>
## Data Preparation
Transform the target variable into a dummy variable (since binary). Split the data into training and test sets. 

The percentage of spam documents in the entire dataset is 13.4%. 

In the data analysis, we have compared spam and not spam documents over some important factors that will be used later as additional features in the classification problem. In particular, we found important differences in:
* The average **length of documents** (number of characters). 138.87 for spam and 71.02 for non-spam.
* The average **number of digits** per document: 15.76 for spam and 0.30 for non-spam.
* The average number of non-word characters (anything other than a letter, digit or underscore) per document: 29.04 for spam and 17.29 for non-spam.


<a id='classificationmodels'></a>
## Classification Models

In any NLP (Natural Language Processing) application, one of the leading choices that have to be made is how to best convert text to numerical representation for running Machine Learning models. 

In this case, we consider two different ways to make the such conversion: a **Count Vectorizer** and a **TF-IDF Vectorizer**. The Count Vectorizer converts a collection of text documents to a matrix of token counts (a frequency representation). In contrast, TF-IDF (Term Frequency - Inverse Document Frequency) Vectorizer converts a collection of raw documents to a matrix of TF-IDF features, which is a statistic based on the frequency of a word in the corpus but also provides a numerical representation of how important a word is for statistical analysis. TF-IDF usually performs better than Count Vectorizers because it considers the words' importance, removing less critical terms and lowering complexity by reducing dimensionality.

For both Vectorizers, we consider two different approaches: **Bag-of-words** and **N-grams**. In Bag-of-words models, the text is represented as the bag of its words, disregarding grammar and word order. In N-Gram models, we consider a connected string of N items (weighing the structure and connection between words). Conceptually, we can view the bag-of-word model as a special case of the n-gram model, with n=1. 

Depending on the choice of Vectorizer and bag-of-words/n-gram, we consider four different transformations of the initial dataset. Three different classification algorithms are used for each of these transformed datasets (**Multinomial Naive Bayes**, **Support Vector Classifier**, and **Logistic Regression**). Each ML model is tuned using **Grid Search** (considering accuracy to evaluate the performance). 


<a id='results'></a>
## Results

![res](https://user-images.githubusercontent.com/80990030/191803317-6eb29a92-7bb3-4931-bf1c-31a41141079a.png)

The classification model with the higher performance is the **Support Vector Classifier** with **C=1000** and **gamma=0.001**, using the **bag-of-words** data with the **Count Vectorizer** (the results are, however, similar between different combinations). The **test accuracy** achieved by the such model is **99.2%**, and the **AUC score** is equal to **0.9778**. The performance of such a combination is surprising since it uses the more straightforward options considered in the data transformation.

![conf_matrix](https://user-images.githubusercontent.com/80990030/191802857-951dae3f-521f-40dc-a72d-89e7b26f0593.png)

![ROC](https://user-images.githubusercontent.com/80990030/191802903-a251186f-8fdd-4905-94ff-b1af035cc433.png)
