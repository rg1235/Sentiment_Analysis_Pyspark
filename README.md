# Sentiment_Analysis_Pyspark
Sentiment analysis of Yelp business review on Pyspark

## Overview
The project aims at predicting the user rating for a business based on sentiment analysis of the review given by the user.
The rating prediction based on the user review will act as a performance parameter thereby,helping comparison of various businesses.

## Goals
The goal is to build a sentiment analysis model that predicts whether a user liked a local business or not, based on their review on Yelp.

## Specifications
Firstly,the classification algorithm will need some sort of feature vector in order to perform the classification task. The simplest way to convert a corpus to a vector format is the bag-of-words approach, where each unique word in a text will be represented by one number.It’s also important to exclude the stop words and punctuation.
The second most important part is vectorisation , which should be carried out in such a manner that for each review we should know the number of times a particular word is used.
Lastly, for classification we can use any of the existing sentiment analysis approaches.Using Mlib library available on spark core engine.

## Dataset Description
The dataset was obtained from Kaggle . The [Yelp dataset](https://www.kaggle.com/c/yelp-recsys-2013/data) was given corresponding to a Business rating prediction problem on Kaggle.
The dataset has the following dimensions:<br/>
>
Training set:<br/>
- 11,537 businesses<br/>
- 8,282 checkin sets<br/>
- 43,873 users<br/>
- 229,907 reviews<br/>
>
Test set:<br/>
- 1,205 businesses<br/>
- 734 checkin sets<br/>
- 5,105 users<br/>
- 22,956 reviews<br/>
>
Each of businesses , users ,checkin sets , reviews are stored in the form of JSON objects , which means it is in a set of sets format.
The file format of the dataset files is .json .The data need to be processed first and then the JSON file can be loaded in order to get a list containing JSON objects.
Another thing which can be done is we can convert the file containing JSON objects into a CSV file.

## Procedure Used

- Procedure involved tokenizing each review using tokenizer class
- To remove stop words we have used stopwordremover class available in pyspark.mllib library
- For this project two types of features have been used: 
  - Bag of words approach (Unigrams)
  - Unigrams + Bigrams (pair of words)
- For feature extraction the following two methods have been used:
  - Count Vectorizer
  - TF-IDF
- The data consists of the following number of samples in each class where stars are referred to as class labels and count as the number of samples<br/>
<br>

|stars|Count
|-----|-----
|  5  |76193
|  1  |17516
|  3  |35363
|  2  |20957
|  4  |79878

- Two types of classifiers have been used Logistic regression with softmax and Multinomial Naive Bayes.
- The following combinations of Features, Feature extraction , classifier have been used :
  - Unigram → Count Vectorizer → Logistic regression
  - Unigram → TF-IDF  → Logistic Regression
  - (Unigram+Bigram) → Count Vectorizer → Logistic regression
  - (Unigram+Bigram) → TF-IDF → Logistic regression
  - Unigram → Count Vectorizer → Naive Bayes
  - Unigram → TF-IDF  → Naive Bayes
  - (Unigram+Bigram) → Count Vectorizer → Naive Bayes
  - (Unigram+Bigram) → TF-IDF → Naive Bayes

## Results
For Unigram i.e bag of words as features , the table indicates the accuracy obtained for the combination of features extraction method and the classifier used :
	
|            |Count Vect.|TF-IDF|
|------------|---------|--------|
|Logistic Reg|49.399%|47.573%|
|Naive bayes|51.255%|48.626%|


For Unigram+Bigram as features the given tables indicates the accuracy obtained for the combination of feature extraction method and the classifier used:
		
|            |Count Vect.|TF-IDF|
|------------|---------|--------|
|Logistic Reg|51.206%|56.146%|
|Naive bayes|54.343%|49.524%|


We can see that using Unigram+Bigrams as features significant performance improvements can be seen as compared to using Unigram as features , which shows that pair of words can have significant impact on sentiment analysis.
