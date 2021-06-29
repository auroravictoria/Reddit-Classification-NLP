
## Report by AV David

<br>

### Problem Statement

I was assigned to collect posts from two different subreddit topics and create a model that can accurately predict which subreddit topic a particular post is from. I selected the following subreddits: hiking and gardening. Using Data Acquisition, Natural Language Processing, and Classification, this report addresses the problem, **"What model best predicts the topic of a subreddit post?"**


---

### Executive Summary

For this project, 7,000 hiking subreddit posts and 5,500 gardening subreddit posts were collected. Texts from actual reddit submissions and comments were used for the modeling. There are many ways to clean the data, so we explored various models on data that was a) minimally cleaned and b) deeply cleaned. Minimally cleaned means that only "deleted" posts were removed and no other cleaning was done. Deeply cleaned means duplicate texts, hyperlinks, emoticons, emojis, and punctuation marks were all removed, and that the text were made lowercase. At the end of deep cleaning, 11,800 posts remained, providing a null baseline accuracy rate of 56% (hiking being 56%, while gardening being 44%).

The following were the pre-processing features, parameters, and estimators that were explored:
1. Text Lemmatization
2. Vectorizing Text - max features, ngram range, and stop words
    - CountVectorizer 
    - TfidfVectorizer
3. Estimators - alpha parameter
    - Logistic Regression
    - Naive Bayes

The metric used to evaluate the models was the balanced accuracy score since accurately predicting both topics is equally important

The following models came out to be the top 2 predictors:


|Estimator|Estimator Parameter|Vectorizer|Vectorizer Parameters|Data Cleaning|Lemmatized|Balanced Accuracy Score|
|---|---|---|---|---|---|---|
|Bayes|<center>alpha = 0.12</center>|CountVectorizer|Max features = 6,700;<br> ngram range=(1,1); <br>removed English stop words|<center>Minimal </center>|<center>No</center>|<center>91.64% </center>
|Bayes|<center>alpha = 0.07</center>|CountVectorizer|Max features = 5,000;<br>  ngram range=(1,1);<br>  removed English stop words|<center>Deep </center>|<center>Yes</center>|<center>91.15% </center>


---

### File Directory

I have included the following in this report:

- README.md
- Datasets folder
    - Data collected using Pushshift's API
    - Postings cleaned (minimally)
    - Posting cleaned (deeply)
    - Model list summary (includes scores and parameters used)
- Code folder
    - Data Collection
    - Data Cleaning and EDA
    - Modeling 1 (Logistic Regression) - after minimal cleaning
    - Modeling 1 (Naive Bayes) - after minimal cleaning
    - Modeling 2 (Logistic Regression) - after deep cleaning
    - Modeling 2 (Naive Bayes) - after deep cleaning
    - Model evaluation and selection
- Presentation folder
    - Presentation pdf

---

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**topic**|*object*|Postings|The subreddit topic where the post is from|
|**text**|*object*|Postings|The text in the post (a submission or a comment)|
|**estimator**|*object*|Model List|The estimator used in the model (Logistic Regression or Naive Bayes)|
|**vectorizer**|*object*|Model List|The vectorizer used (CountVectorizer or TfidfVectorizer)|
|**data_cleaning**|*object*|Model List|Degree of data cleaning (minimal or deep)|
|**lemmatized**|*object*|Model List|Whether text was lemmatized or not|
|**train_acc**|*float*|Model List|The accuracy score of the train data|
|**test_acc**|*float*|Model List|The accuracy score of the test data|
|**train_bal_acc**|*float*|Model List|The balanced accuracy score of the train data|
|**test_bal_acc**|*float*|Model List|The balanced accuracy score of the test data|
|**params**|*object*|Model List|List of parameters used in the model|


---

### Conclusions and Recommendations

Based on the exploration and modeling of the data, below are my findings and recommendations:

1. Use Bayes model. The Bayes models performed better and had a higher balanced accuracy score better than logistic regression models.
2. Be discerning in data cleaning. As we see in the model scores created in this project, more data cleaning does not necessarily mean better models.
3. Lemmatize. For both Bayes and Logistic Regression, lemmatization brought up the balanced accuracy score. 
4. Consider both CountVectorizer and TfidfVectorizer since they both vary in performance depending on the estimators, lemmatization, and other factors.

