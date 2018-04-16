Reading a Text File and saving it as CSV 

```
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

df['agg'] = df['agg'].apply(lambda x: str(x).strip())
```

