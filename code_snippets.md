## Cleaning 
```
ts.dropna(axis=0, how='any', thresh=None, subset=None, inplace=True)
ts.drop_duplicates(keep = 'last',inplace = True)
ts['scrub'] = ts['scrub'].str.replace('[^a-zA-Z\s]','')
ts['scrub'] = ts['scrub'].apply(lambda x: x.strip())
ts['scrub'] = ts['scrub'].apply(lambda x: re.sub(r'\s+', ' ', x))
ts['scrub'] = ts['scrub'].apply(lambda x: x.upper())
ts.drop_duplicates(keep = 'last',inplace = True)
```
# counting number of datapoints in each class 
```
temp['id'] = pd.Series(temp['agg']).astype('category').cat.codes
# numbering starts from 0 in pandas, now add 1 so that numbering starts from 1 
temp.sort_values(by=['id'],ascending=[True],inplace = True)
temp['id'] = temp['id'].apply(lambda x: x+1)
cnt = temp.groupby('id').count().reset_index()
cnt.drop(cnt.columns[[1,3,4,5,6]], axis=1, inplace=True)
counts = cnt.loc[(cnt['agg'] > 9) & (cnt['agg'] <= cnt['agg'].max())]
new = temp.loc[temp['id'].isin(counts['id'])]
new.drop_duplicates(keep = 'last',inplace = True)
test = new.sample(frac = 0.2)
train = new[(~new.bnm.isin(test.bnm))]
new_train = (train.groupby(['agg', 'chn'])['bnm'].apply(lambda x: x if (len(x) <=30) else x.sample(30)).reset_index(level=2, drop=True).reset_index())
new_test = test.loc[test['id'].isin(counts['id'])]
bigrams = pd.read_pickle('bigrams.pkl')
# chn = pd.read_pickle('chn.pkl')
bigram_vectorizer = CountVectorizer(analyzer='char', ngram_range=(2, 2), token_pattern=r'\b\w+\b', min_df=1)
countvec1 = CountVectorizer()
# countvec2 = CountVectorizer()
big_dtm = bigram_vectorizer.fit_transform(bigrams.bigrams)
new_train['bnm'].fillna(' ',inplace=True)
import re
```
## reading a text file in pandas
```
data = '...txt'
import codecs
file = codecs.open(data, "r",encoding='utf-8', errors='ignore')
lines = file.read().split("\n")

a = []
b = []
c = []
d = []
e = []
for s in range(0,len(lines)-1):
    l = lines[s].split("|")
    if len(l) == 5:
        a.append(l[0].strip().replace('\x00',''))
        b.append(l[1].strip())
        c.append(l[2].strip() + ' ')
        d.append(l[3].strip() + 'M')
        e.append(l[4].strip())

df = pd.DataFrame(
    {'cbsnm': a,
     'chn': b,
     'ctg': c,
     'mcc': d,
     'agg': e
    })

```
## computing jaccard distance 
```
from sklearn.metrics.pairwise import pairwise_distances
def jaccard(a,b,n):
 s = [a[i:i+n] for i in range(len(a)-n+1)]
 t = [b[i:i+n] for i in range(len(b)-n+1)]
 if len(list(set(s) | set(t))) >0:
  jac_coeff = 1 -  len(list(set(s) & set(t))) / len(list(set(s) | set(t)))
 else:
  jac_coeff = 1
 return jac_coeff

result_df1['sim'] = result_df1.apply(lambda x:jaccard(x[0], x[6], 2), axis = 1)
```
##
```
