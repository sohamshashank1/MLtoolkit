## Identifying if its Name of a person or Business Entity using Stanford NER Parser in Python 
### Sample code 

```
os.chdir("...")
ner_file = pd.read_csv("...", sep =",", header = None, encoding='latin-1')
ner_sample = ner_file.sample(frac=0.00005)
ner_sample.columns = ['name']
ls = ner_sample['name'].tolist()
s = list()
from nltk.tag import StanfordNERTagger
from nltk.tokenize import word_tokenize

st = StanfordNERTagger('...')
ms2 = pd.DataFrame()
master = pd.DataFrame()
for s in range(0,len(ls)):
    l1 = st.tag(str(ls[s]).split())
    l2 = []
    for r in range(0,len(l1)):
        l2.append(l1[r][1])
    l2 = list(set(l2))
    if(len(l2) >1):
        if('ORGANIZATION' in l2):
            a = 'ORGANIZATION'
        elif('PERSON' in l2):
            a = 'PERSON'
        else:
            a = 'O'
    else:
        a = l2[0]
    ms1 = pd.DataFrame({'bsn': ls[s], 'tag': a }, index=[0])
    master = master.append(ms1)
```
-----------------------------------------------------------------------------------------------

```
mylist  = pd.read_csv()
mylist.columns = ['ids', 'name']
ids = mylist['ids'].tolist()
names = mylist['name'].tolist()
r = list()
for i in range(0,len(names)):
    s = word_tokenize(names[i])
    for t in range(0,len(s)):
        r.append(s[t])
dic_full = pd.DataFrame(r)
dic_full.columns = ['NAME']
dictionary = dic_full.sample(frac = 0.6)

p = list()
for i in range(0, len(names)):
    s = word_tokenize(names[i])
    m = 0
    for j in range(0,len(s)):
        if dictionary['NAME'].str.contains(s[j]).any():
            m = m+1
    if m == len(s):
        p.append(1)
    else:
        p.append(0)

flag = pd.DataFrame(p)
flag.columns = ['flag']
final = pd.concat([mylist.reset_index(drop=True), flag.reset_index(drop=True)], axis = 1)
