![Figure 0](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image001.png)

## Introduction

The data is from: https://www.kaggle.com/datatattle/covid-19-nlp-text-classification.

The dataset is summarised to two columns includin original tweets and the related sentiments classification. The data resulted quite balanced regarding the sentiments distribution overall: ‘Positive’=‘Negative’, ‘Extremely Positive’=’Extrememly Negative’ and ‘Neutral’.(Figure 1)

![Figure 1](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image004.png)
Figure 1

## Lexicon Based Future Extraction

The positive and negative sentiments are balanced by the classification of the words in all of the lexicons. However, to decide which lexicon has the strongest relation to the sentiments, one can measure the mean values. From this aspect, for instance, afinn lexicon( see Figure 2, 3rd raw) has average of 4.5 positive words for sentiment ‘extremely positive’ and 2 words for sentiment ‘positive’ whilst the other lexicons have roughly half of the mean values for the same sentiments. Nevertheless, the data is quite reasonable for each lexicons and have strong relation to the sentiments. Distinguishing negative and positive sentiments based on simple lexicon features seems very reasonable. Simple counting based strategies are likely to work.

![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image005.png)
![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image007.png)
![Figure 2](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image009.png)

Figure 2

## Text Cleaning Steps 
The text has cleaned form urls, mentions, hashtags, punctuations, emojis and digits which are neutral and does not have much sentimental meaning. All of the words are lowercased to avoid duplicated words to results as different token. Moreover, stop words are removed except "n't", "not", "no" since they can contribute to sentiments when combined with tokens.

## Representatives

### 1-BoW( Bag of Words)
The BoW method helped us to determine the frequency of the words that appears in all tweets (see figure 3). The result is quite reasonable since the date of that particular tweeter dataset is the time when ‘covid’ pandemic raised. The spread of ‘corona virus’  created nations wide ‘panic’ and ‘people’  emptied  the ‘stores’, ’grocery’ and ‘supermarkets’ to ‘stock’ ‘food’   and stay home quarantine to avoid getting sick.  

![Figure 3](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image011.png)
Figure 3 

There are other type of representation rather than the classic The Bag of Words (BoW) model. However, the BoW is the simplest form of text representation in numbers. Like the term itself, we can represent a sentence as a bag of words vector (a string of numbers). However there are some more requirements to be able to make a sophisticated NLP models. For instance, in BoW model we are retaining no information on the grammar of the sentences nor on the ordering of the words in the text.  Therefore there are other approaches such as Gensim and TF-IDF (Term Frequency-Inverse Document Frequency). The TF-IDF model contains information on the more important words and the less important ones as well. Gensim is a uses top academic models to perform complex tasks like building document or word vectors, corpora and performing topic identification and document comparisons. word embedding or vector is trained from a larger corpus and is a multi-dimensional representation of a word or document. With these vectors, we can then see relationships among the words or documents based on how near or far they are and also what similar comparisons we find.
### 2. TF-IDF with Gensim

The implementation of the related method is performed as creating a dictionary that gave id numbers to every words, for instance ‘neighboor’= 13.  This allowed to determine most important words in each tweets by identification numbers. Each corpus may have shared words beyond just stopwords and these words should be down-weigted in importance. In our case the covid must not show up as a key word and it is down-weighted. On the example tweet below: 

*Coronavirus Australia: Woolworths to give elderly, disabled dedicated shopping hours amid COVID-19 outbreak*

The tweet have covid and coronavirus as two of the most frequent words used in BoW. On the other hands the tweet specific frequent words are weighted high as shown in the Figure 4 which highlights only the most relevant words that one can understand the meaning of the tweet without reading total sentence.


![Figure 4](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image013.png)

Figure 4 

## Trained Classifier

### 1. Logistic Regression

To train the models, we use CountVectorizer to convert words to numbers by assigning them an id and counting word frequencies and we use a 5-fold crossvalidation approach to estimate the models.
Evaluation metrics are classification matrix as precision, recall and F1 score.
Parameters for vectorizers:

•	max_df: maximum document frequency (e.g., 0.5 or maximum document frequency of 50%).

•	min_df: how many sentences need to contain the words (e.g., 1 or the words need to appear in at least 2 sentences)

•	ngram_range: (1, 2), both single words as bi-grams are used

Parameters for logistic regression:

clf__penalty: {‘l1’, ‘l2’, ‘elasticnet’, ‘none’}, default=’l2’: Used to specify the norm used in the penalization. clf__C: float, default=1.0: Inverse of regularization strength; must be a positive float. Like in support vector machines, smaller values specify stronger regularization.

### 2. Results 

From the Figure 5 we can see the model has good numbers when it comes to predict class ‘Extremely Negative’ or ‘Extremely Positive’, but not that good for predicting ‘Negative’ and ‘Positive’. With the Neutral, we have a precision of 58%, and a recall of 91%, resulting in an F1 score of 0.71.

![Figure 5](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image015.png)

Figure 5 

Below table shows some tweet samples including the real sentiment and predicted ones according to our best model

![Figure 6](https://github.com/tekinuyan/ML-Studies/blob/main/Sentiment%20Analysis%2C%20%20NLP/A4_Tekin_uyan_601991_Report_pics/image016.png)
