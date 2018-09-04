## collections.Counter()

> A Counter is a dict subclass for counting hashable objects. It is an unordered collection where elements  are stored as dictionary keys and their counts are stored as dictionary values. Counts are allowed to be any integer value including zero or negative counts. The Counter class is similar to bags or multisets in other languages.

```python
import collections
lst = ['cc', 'cc', 'dd', 'aa', 'bb', 'ee']
print(collections.Counter(lst))
'''
Counter({'cc': 2, 'dd': 1, 'aa': 1, 'bb': 1, 'ee': 1})
'''
```
갯수가 많은 것 부터 출력해준다.
```python
import collections
container = collections.Counter()
container.update("my name is Danial")
print(container)
'''
결과
Counter({' ': 3, 'a': 3, 'm': 2, 'n': 2, 'i': 2, 'y': 1, 'e': 1, 's': 1, 'D': 1, 'l': 1})
'''
for k,v in container.items():
print(k,':',v)
'''
결과
m : 2
y : 1
  : 3
n : 2
a : 3
e : 1
i : 2
s : 1
D : 1
l : 1
'''
```

### Counter.update()
Counter의 값을 갱신한다.
```python
import collections
# 문자열
a = collections.Counter()
print(a)
a.update("my name is Danial")
print(a)
'''
결과
Counter()
Counter({' ': 3, 'a': 3, 'm': 2, 'n': 2, 'i': 2, 'y': 1, 'e': 1, 's': 1, 'D': 1, 'l': 1})
'''
# 딕셔너리
a.update({'a':3, 'm':2})
print(a)
'''
결과
Counter({'a': 6, 'm': 4, ' ': 3, 'n': 2, 'i': 2, 'y': 1, 'e': 1, 's': 1, 'D': 1, 'l': 1})
'''
```
