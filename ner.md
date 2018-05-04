# searching for person names from a dictionary of person names and tagging it (True/ False)
```
# creating sample dictionary 
from nltk.tokenize import word_tokenize
r = list()
for i in range(0,len(dct_list)):
    s = word_tokenize(dct_list[i])
    for t in range(0,len(s)):
        r.append(s[t])
dic_full = pd.DataFrame(r)
dic_full.columns = ['NAME']
dic_full['NAME'].drop_duplicates(keep = 'last',inplace = True)
# checking if its a name 
p = list()
for i in range(0, len(bus_nm)):
    s = word_tokenize(bus_nm[i])
    m = 0
    for j in range(0,len(s)):
        if dic_full['NAME'].str.contains(s[j]).any():
            m = m+1
    if m == len(s):
        p.append(1)
    else:
        p.append(0)

flag = pd.DataFrame(p)
flag.columns = ['flag']
final = pd.concat([bus.reset_index(drop=True), flag.reset_index(drop=True)], axis = 1)
```
