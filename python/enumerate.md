## Enumerate
enumerate는 for문과 함께 사용하면 리스트 데이터의 인덱스값과 밸류값을 따로 확인할 수 있다는 장점이 있다.

```python

for i, N in enumerate(['body', 'foo', 'bar']):
    print(i, name)

# output
'''
0 body
1 foo
2 bar
'''

for i, N in enumerate([1, 2, 20]):
    print("i = " + str(i))
    print("N = " + str(N))

# output
'''
i = 0
N = 1
i = 1
N = 2
I = 2
N = 20
'''

```
