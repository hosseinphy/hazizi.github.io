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
The estimated R<sup>2</sup> =  0.64 and RMSE =  0.79


## Word polarity
Another apprpach to derive some insights from our data is the Polarity Analysis which can offer a simplistic view of the sentiment information,
based on the polarity of the words in a given sentence. The aim of this model is to identify the most "polarizing words" in the corpus of reviews that strongly signal positive (five-star), or negative (one-star) reviews. 

### Model
We employed [naive Bayes model](https://scikit-learn.org/stable/modules/naive_bayes.html#) to calculate a **polarity score** for each word $w$,
$\textrm{polarity}(w) = \log\left(\frac{Pr(w\ |\ \textrm{positive})}{Pr(w\ |\ \textrm{negative})}\right).$ Naive Bayes models can offer some major advantages, including their higher explicability compared to more complex models, they are easy to train, and a parallelizable training process.


The model is constructed using the following steps:
1. Isolate the reviews with highest and lowest stars, which should contain the most polarizing words.
2. Used `MultinomialNB` naive Bayes model to train on feature matrix of the most polar reviews (created by TfidfVectorizer with TF-IDF weighting and removing stop words).
3. Calculate the probability of words in the vocabulary, and extract the most polar ones.


### create polar data
```python
# Create the most polar reviews and labels
pos_data = [row['text'] for row in data if row['stars'] == 5 ]
neg_data = [row['text'] for row in data if row['stars'] == 1 ]
polar_data = pos_data + neg_data

labels = ['positive'] * len(pos_data)  + ['negative'] * len(neg_data)
```


### Build pipeline

```python 
pipe = Pipeline([
                ('tvec', TfidfVectorizer(
                                        stop_words=stop_words_lemma,
                                    )
                ), 
                ('mnb', MultinomialNB())
        ])

 
pipe_parameters = {
    'tvec__min_df' : [0.0001, 0.001, 0.01],
    'tvec__max_df' : [0.9, 0.99, 0.999],
    'tvec__max_features' : [3000, 5000]    
}

gs = GridSearchCV(pipe, pipe_parameters, cv=2, n_jobs=-1)
gs.fit(polar_data, labels);
```

```mark
this is the worst nail salon in the city i ve been twice and twice the nail chick different one each time made me bleed this time she destroyed my cuticles i couldn t even wear closed toe shoes without feeling pain and 40 bucks for a pedi that s way too much and she did a \x1b[41m\x1b[37mhorrible\x1b[0m job the polish wasn t even put on neatly and correctly and she was \x1b[41m\x1b[37mrude\x1b[0m as hell i really wanted to kick her while she was down there mangling my \x1b[41m\x1b[37mpoor\x1b[0m feet up'
```

```markdown
![](https://img.shields.io/static/v1?label=&message=awesome&color=green) service they had an ![](https://img.shields.io/static/v1?label=&message=awesome&color=green) drink called the ginger beast when we came to eat here we asked for it it s no longer on the menu they stopped serving it a few months ago according to our waitress but she asked the barkeep and the bar was willing to make it for us ![](https://img.shields.io/static/v1?label=&message=awesome&color=green) service the food here is top notch fresh and wow yummo the oyster tasting shooters are great the shibuya roll is great the shibaki tuna tartare is great the pork crisp is yummy and the black cod wow ![](https://img.shields.io/static/v1?label=&message=awesome&color=green) and did i mention how good the shibuya roll is it was so good that we had to order another one ![](https://img.shields.io/static/v1?label=&message=awesome&color=green) place inside the mgm grand
```



![](https://img.shields.io/static/v1?label=&message=awesome&color=green)
![](https://img.shields.io/static/v1?label=&message=notch&color=green)





## Conclusion
