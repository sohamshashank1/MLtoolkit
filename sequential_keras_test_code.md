## Reading file 
```
import pandas as pd
import os
import tensorflow as tf
tr = pd.read_csv("rnn_train.csv")
import os
import pandas as pd
from scipy import sparse, io
from scipy.sparse import coo_matrix, hstack, vstack
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.ensemble import RandomForestClassifier
from sklearn.externals import joblib

import keras
from keras.models import Sequential
from keras.layers import Dense, Dropout, Activation
```
## Creating a standard bigram for creating a document term matrix
```
os.chdir('')
bigrams = pd.read_pickle('bigrams.pkl')
chn = pd.read_pickle('chn.pkl')
ctg = pd.read_pickle('ctg.pkl')
 mcc = pd.read_pickle('mcc.pkl')
bigram_vectorizer = CountVectorizer(analyzer='char', ngram_range=(2, 2), token_pattern=r'\b\w+\b', min_df=1)
countvec1 = CountVectorizer()
countvec2 = CountVectorizer()
countvec3 = CountVectorizer()
big_dtm = bigram_vectorizer.fit_transform(bigrams.bigrams)
chn_dtm = countvec1.fit_transform(chn.chn)
ctg_dtm = countvec2.fit_transform(ctg.ctg)
mcc_dtm = countvec3.fit_transform(mcc.mcc)
train_dtm = bigram_vectorizer.transform(tr.cbsnm)
train_chn_dtm = countvec1.transform(tr.chn)
train_ctgy_dtm = countvec2.transform(tr.ctg)
train_mcc_dtm = countvec3.transform(tr.mcc)
```
## Combining dtm into one 
```
dtm_final_train = hstack([train_dtm, train_chn_dtm, train_ctgy_dtm,train_mcc_dtm])
```
## converting classes into categories 
```
labels = tr['agg']
one_hot_labels = keras.utils.to_categorical(labels, num_classes=None)
one_hot_labels.shape
```
## DTM into dtm array 
```
dtm_train_a = dtm_final_train.A
```
## Defining a sequential model 
```
from keras.models import Sequential
from keras.layers import Dense, Dropout, Activation
model = Sequential()
model.add(Dense(6264, activation='relu', input_dim=1836))
model.add(Dropout(0.5))
model.add(Dense(5398, activation='softmax'))
model.compile(optimizer='rmsprop',loss='categorical_crossentropy',metrics=['accuracy'])
model.fit(dtm_train_a, one_hot_labels, epochs=10, batch_size=600)
```
