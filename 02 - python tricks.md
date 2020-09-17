# 2. Python Tricks

## 2.1 Find Top Earners


```python
employees = {'Alice':100000,
            'Bob': 95000,
            'Carol': 80000,
            'Dave': 120000}
```


```python
# Find all employees over 100000
# One solution

top_earners = []
limit = 100000
for key, val in employees.items():
    if val >= limit:
        top_earners.append((key,val))

print(top_earners)
```

    [('Alice', 100000), ('Dave', 120000)]


OneLine solution using list comprehension.

List comprehension:
`[Expression + Context]`

e.g:

`[x**2 for x in range(10)]`


```python
[x**2 for x in range(10)]
```




    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]




```python
[(k,v) for (k,v) in employees.items() if v >= limit]
```




    [('Alice', 100000), ('Dave', 120000)]



## 2.2 Find words with high information value


```python
# filter out all words with len <= 3
text = '''
Some books deserve to be held aloft and pointed to as an example of factual correctness. 
These books are valuable resources. Other books take liberties with the facts, or present alternate truths. 
This is especially true of books that rely on people’s memories with little corroborating evidence to back it up
'''
```


```python
# get all words
w = [[x for x in line.split() if len(x) >3]  for line in text.split('\n')]
```


```python
print(w)
```

    [[], ['Some', 'books', 'deserve', 'held', 'aloft', 'pointed', 'example', 'factual', 'correctness.'], ['These', 'books', 'valuable', 'resources.', 'Other', 'books', 'take', 'liberties', 'with', 'facts,', 'present', 'alternate', 'truths.'], ['This', 'especially', 'true', 'books', 'that', 'rely', 'people’s', 'memories', 'with', 'little', 'corroborating', 'evidence', 'back'], []]


## 2.3 Open a file and read by line


```python
print([line.strip() for line in open('test.txt')])
```

    ['Some books deserve to be held aloft and pointed to as an example of factual', 'correctness.', 'These books are valuable resources.', 'Other books take liberties with the facts, or present alternate truths.', 'This is especially true of books that rely on people’s memories with little', 'corroborating evidence to back it up.']


## 2.4 map and lambdas


```python
txt = ['lambda functions are anonymous', 'anonymous dont have a name', 'some gibberish']
```


```python
# one line
mark = map(lambda s: (True,s) if 'anonymous' in s else (False,s),txt)
```


```python
print(list(mark))
```

    [(True, 'lambda functions are anonymous'), (True, 'anonymous dont have a name'), (False, 'some gibberish')]


## 2.4 Exercise: Use list comprehension instead of map


```python
mark = [(True,s) if 'anonymous' in s else (False,s) for s in txt]
```


```python
print(mark)
```

    [(True, 'lambda functions are anonymous'), (True, 'anonymous dont have a name'), (False, 'some gibberish')]


## 2.5 Find text


```python
letters_amazon = '''
 We spent several years building our own database engine,
 Amazon Aurora, a fully-managed MySQL and PostgreSQL-compatible
 service with the same or better durability and availability as
 the commercial engines, but at one-tenth of the cost. We were
 not surprised when this worked.
 '''

```


```python
"my name is".find("name")# returns the index of the first occurence
```




    3




```python
# find a given string in the text +- 18 character before and after

find = lambda x,q:x[x.find(q)-18 : x.find(q)+18] if q in x else -1
```


```python
find(letters_amazon,'SQL')
```




    'a fully-managed MySQL and PostgreSQL'



## 2.6 Combine list comprehension and slicing


```python
## Data (daily stock prices ($))
price = [[9.9, 9.8, 9.8, 9.4, 9.5, 9.7],
[9.5, 9.4, 9.4, 9.3, 9.2, 9.1],
[8.4, 7.9, 7.9, 8.1, 8.0, 8.0],
[7.1, 5.9, 4.8, 4.8, 4.7, 3.9]]

```


```python
# include only every second item
new_price = [line[::2] for line in price]
```


```python
new_price
```




    [[9.9, 9.8, 9.5], [9.5, 9.4, 9.2], [8.4, 7.9, 8.0], [7.1, 4.8, 4.7]]



## 2.7 Slicing and assignments


```python
data = ['Firefox','corrupted','Chrome','corrupted', 'Edge','corrupted']
# every other item is corrupted, recplace with previous item
data[1::2] = data[::2]
```


```python
data
```




    ['Firefox', 'Firefox', 'Chrome', 'Chrome', 'Edge', 'Edge']



## 2.8 


```python
## Dependencies
import matplotlib.pyplot as plt
## Data
cardiac_cycle = [62, 60, 62, 64, 68, 77, 80, 76, 71, 66, 61, 60, 62]

```


```python
plt.plot(cardiac_cycle)
```




    [<matplotlib.lines.Line2D at 0x7f64b814b550>]




![png](02%20-%20python%20tricks_files/02%20-%20python%20tricks_33_1.png)



```python
# generate a bigger cycle (10 times), but the first two and last values are redundant
clean_cycle = cardiac_cycle[1:-2]
plt.plot(clean_cycle)
```




    [<matplotlib.lines.Line2D at 0x7f64b80db810>]




![png](02%20-%20python%20tricks_files/02%20-%20python%20tricks_34_1.png)



```python
rep_cycle = clean_cycle * 10
```


```python
plt.plot(rep_cycle)
```




    [<matplotlib.lines.Line2D at 0x7f64b85de610>]




![png](02%20-%20python%20tricks_files/02%20-%20python%20tricks_36_1.png)



```python
companies = {
 'CoolCompany' : {'Alice' : 33, 'Bob' : 28, 'Frank' : 29},
 'CheapCompany' : {'Ann' : 4, 'Lee' : 9, 'Chrisi' : 7},
 'SosoCompany' : {'Esther' : 38, 'Cole' : 8, 'Paris' : 18}}

```


```python
illegal = [x for x in companies if any(y<9 for y in companies[x].values())]
```


```python
print(illegal)
```

    ['CheapCompany', 'SosoCompany']



```python

```
