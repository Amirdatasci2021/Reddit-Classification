# Project 3: Web APIs & Classification
## Natural Language Processing & Ideology:
### A mechanical inference on the pathology of words

In the academic disciplines that deal with language, a natural language or how we talk the natural which has evolved with people throughout our short stay on this planet through use and repetition. Natural Language Processing, is the aspect of artificial intelligence that deals with the interaction between computers and humans using the natural language.

While the bulk of what is done in this project may relate to machines it is an inflection on us. We might learn something about ourselves. 

### Problem Statement:

Can Natural Language Processing with help of SKLearn distinguish between two ideologically oppositional subreddits? Can my models find the comments and submissions form r/mensrights?

### Subjects:

Two ideologically opposed, adversarial and extremely parallel subreddits:

r/MensRights
https://www.reddit.com/r/MensRights/

r/Feminism
https://www.reddit.com/r/Feminism/

### Objective
To validate that ideology can be infered without context using different models and NLP to provide some level of possibility in the existence of ideological paradigms in text. Understanding our objective we are seeking to demonstrate that ideological preference is visible or not visible in a simple machine learning model and that it can or can not accurately predict what subreddit it came from. As for our baseline, our fundamental assumption is that anything close to .5 would be as good as it calling it out randomly or flipping a coin. 


## Executive Summary:

Table of Contents:
|File name  | Link  |
|--|--|
| Collector.ipynb | https://github.com/Amirdatasci2021/Reddit-Classification/blob/master/collector.ipynb |
| DataFrame_Femenism.ipynb |https://github.com/Amirdatasci2021/Reddit-Classification/blob/master/DataFrame_Femenism.ipynb  |
| DataFrame_Mensrights.ipynb | https://github.com/Amirdatasci2021/Reddit-Classification/blob/master/DataFrame_Mensrights.ipynb |
| logreg demo.ipynb | https://github.com/Amirdatasci2021/Reddit-Classification/blob/master/logreg%20demo.ipynb |
| SVM demo.ipynb |https://github.com/Amirdatasci2021/Reddit-Classification/blob/master/SVM%20demo.ipynb  |


Data contains 3 folders:
fem(data collected r/Feminism) 
men(r/MensRights) 
z_collect(final cleaned prepped products)

### Process

Using pushshift.io API to collect large enough datasets from the designated subreddit posts above. Pushshift has some pretty unclear rules so the method was to make repeated small calls for information based on the utc_creation timestamp as a way to repeat the process to collect more information. Both the submissions and the comments were used for text samples. Each file was collected in it's own folder. An additional feminism post was mixed in for a later expirement that was never reached of seeing if the models could detect where the origin was regardless. Feminism had 19891 rows of data and 


### Data Cleaning and EDA:

The following were removed from the submission/comments: markup hyperlinks, punctuation, numbers, special characters, all digits, carriage returns, newlines, tabs, and “amp”. This was done with regex, .replace and NumPy nans. Considering the duplicate were bot messages are still a part of the thread I had mixed feelings about removing them.  After cleaning, there were 4340 for r/MensRights and 8550 for r/feminism. There were a total of 12890 records total, there was a disproportionate number of the two classes. Words were not lemitized or stemmed but some additional stop words were added to the count vectorizer and the TfidfVectorizer to get a better idea for the lexicon analysis. Preliminary EDA showed that they both had very similar most frequent words in both of these classes and they both had very similar sentiment analysis courtesy of Textblob.


### Preprocess and Modeling 
CountVectorizer and TfidfVectorizer from scikit-learn were used to convert the text data to numeric features. TfidfVectorizer achieved a better accuracy score with logistic regression model.

|   | precision  | recall   | f1-score  | support |
|---|---|---|---|---|
| Mensrights   |  0.940278  |0.975018   |0.957333   |  2842 |
| Not Mensrights  | 0.945677  | 0.875354  |  0.909158  |  1412  |
| accuracy | 0.941937  | 0.941937  |  0.941937 |  0.941937   |
 macro avg      |    0.942978 | 0.925186 |   0.933245 | 4254     |
weighted avg   |    0.94207  | 0.941937 |   0.941342 | 4254  |

Support Vector Machine models were tested with Gridsearch and the time constraints made it impossible to really use it so we used a depricated bestparams with the SVM model. Logistic regression performed the best but both worked very well. The essential problem was the insanely long time that SVM took with running. In an attempt to improve results with SVM I did cut the smaple sizes down but it was still taking too long. 

## Conclusion

Did we gain any insight to text without full context delivering to a machine an ideological paradigm. Yes.
 
So can my models find mensrights(group b)? Despite similarities in sentiment, similar words or overall focus on the same subject a machine
can and is able to distinguish them? Yes.

Can Natural Language Processing with help of SKLearn distinguish between two ideologically oppositional subreddits? Yes, they can.

This means that there is to a lesser or greater degree ideology embedded in language.

Potential improvements for future: would be to collect more training data from more simalar sources that are ideologically similar, do more data cleaning to expunge filler words and expirement with Vader and Nltk, and to use intensive gridsearching to optimize for other models such as L1 and L2 Logistic regressions, Random forest, and Multinomial naive Bayes and explore boosting.
