---
layout: single
title: "Sentiment Analysis"
date: 2021-11-19 12:00:00 -0000
categories: web scraping  nlp  
excerpt: Extract the sentiment form text data.
---

In this project, our objective is to extract sentiment form more than 250000 Yelp review data. We build and train a model that can predict rating of reviews based on the text of reviews. Another approch is to look at the polarity of words. We deployed a naive Bayes model to claculate the polarity of words.





## Data
```markdown
{
'votes': {'funny': 0, 'useful': 0, 'cool': 0}, 
'user_id': 'tYwzsMLMc8juCuIMDAx3dw', 'review_id': 'QsrzjenckNACuOgaEiMWfA', 'stars': 4, 'date': '2011-08-18', 'text': 'Nice simple homey diner. Very friendly staff, huge family friendly menu, salad bar. If you are on the road this beats the same old options.', 'type': 'review', 'business_id': 'uGykseHzyS5xAMWoN6YUqA'}

```

## Bigram_model
```python
params

pipe_feature = Pipeline([
                ('column_transformer', ColumnSelectTransformer(['text'])),
                ('tfidf_vect', TfidfVectorizer(max_features=3000,                                
                                    min_df=0.001,
                                    max_df= 0.99,
                                    preprocessor=pre_processor,
                                    ngram_range=(1,2),
                                    stop_words=stop_words_lemma,
                                    tokenizer=tokenize_lemma, token_pattern=None # or default tokenizer (sklearn)
                        )),
            ])



param_grid = {'alpha': np.logspace(-1, 1, 5)}
gs = GridSearchCV(Ridge(), param_grid)    
pipe_lr = Pipeline([('feat', pipe_feature), ('lr_gs', gs)])     
```


## Word polarity
### create labels based on the reviews
```python
def create_labels(doc):
    tmp = ['positive' if row['stars'] == 5 else 'negative' if row['stars'] == 1 else None for row in doc]
    return [item for item in tmp if item != None]

labels = create_labels(data)
```python

