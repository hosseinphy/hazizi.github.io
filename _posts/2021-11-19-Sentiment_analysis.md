---
layout: single
title: "Sentiment Analysis"
date: 2021-11-19 12:00:00 -0000
categories: web scraping  nlp  
excerpt: Extract the sentiment form text data.
---

In this project, our objective is to extract sentiment form more than 250000 Yelp review data. We build and train a model that can predict rating of reviews based on the text of reviews. Another approch is to look at the polarity of words. We deployed a naive Bayes model to claculate the polarity of words.


## Data format
The training data that are a series of JSON objects were downloaded from aws s3 bucket, and then converted into a list of dictionaries `data` using  [`ujson`](http://docs.micropython.org/en/latest/library/ujson.html) library. A sample review data format is shown below:

```markdown
{
'votes': {'funny': 0, 'useful': 0, 'cool': 0}, 
'user_id': 'tYwzsMLMc8juCuIMDAx3dw', 
'review_id': 'QsrzjenckNACuOgaEiMWfA', 
'stars': 4, 
'date': '2011-08-18', 
'text': 'Nice simple homey diner. Very friendly staff, huge family friendly menu, salad bar. If you are on the road this beats the same old options.', 
'type': 'review', 
'business_id': 'uGykseHzyS5xAMWoN6YUqA'
}
```

The target labels (i.e. *stars*) are pulled from data and saved in a separate list.

## Data preprocessing
To slightly clean up the text, we remove special characters: 
```python
def pre_processor(doc):
    doc = re.sub("(\\W)+"," ",doc)
    return doc
```
This function can be provided as a paramter of TfidfVectorizer

## Feature engineering
  - Stop words, tokenization and Lemmatization are done using spaCy, as shown in the snippet below.   
   - We considered apperence of both single words and pairs of consecutive words (bi-grams).
   - Using the __tf-idf__ values of words or n-grams.

```python
from spacy.lang.en.stop_words import STOP_WORDS
nlp = spacy.load('en')

def tokenize_lemma(text):
    return [w.lemma_.lower() for w in nlp(text)]

stop_words_lemma = set(tokenize_lemma(' '.join(STOP_WORDS)))
```

## Bigram_model

### Hyperparamters
The selected hyperparamters for this model are those that control the vocabulary in the tokenization step (`max_features`, `min_df`, `max_df`)
and the regularization of the regression estimator (`alpha`). To determine these paramters we used [`GridSearchCV`](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html#sklearn.model_selection.GridSearchCV). 

### Data transformation 
Since we aimed to predict star values of reviews based on their text, we built a custom scikit-learn transformer (`ColumnSelectTransformer`) that returns a list of text of all reviews from all records.

The snippet below shows a pipeline that will transform the data from records all the way to predictions, where the hyperparamter tuning is only operating on an `Ridge` estimator that was fed to `GridSearchCV`.

```python
pipe_feature = Pipeline([
                ('column_transformer', ColumnSelectTransformer(['text'])),
                ('tfidf_vect', TfidfVectorizer(max_features=mf,  # mf: optimal max_features                             
                                    min_df=mn,                   # mn: optimal min_df
                                    max_df=mx,                   # mx: optimal max_df
                                    preprocessor=pre_processor,
                                    ngram_range=(1,2),
                                    stop_words=stop_words_lemma,
                                    tokenizer=tokenize_lemma, token_pattern=None # or default tokenizer (sklearn)
                        )),
            ])



param_grid = {'alpha': np.logspace(-1, 1, 5)}
gs = GridSearchCV(Ridge(), param_grid)    
pipe_lr = Pipeline([('feature', pipe_feature), ('lr_gs', gs)])  

pipe_lr.fit(data, stars);
```
The estimated R<sup>&R;</sup>2 = &theta;<sub>o</sub> x + &theta;<sub>1</sub>x

The estimated RMSE: 0.79

## Word polarity
### create labels based on the reviews
```python
def create_labels(doc):
    tmp = ['positive' if row['stars'] == 5 else 'negative' if row['stars'] == 1 else None for row in doc]
    return [item for item in tmp if item != None]

labels = create_labels(data)
```python

