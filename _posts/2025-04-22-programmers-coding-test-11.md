---
layout: single
title: 코딩테스트 암기사항 10.
---

```python
from collections import Counter

def solution(lines):
    counter = Counter() # 비어 있는 Counter 객체로 초기화, 기본적으로 빈 딕셔너리와 비슷
    
    for start, end in lines:
        for i in range(start, end):
            counter[i] += 1
            
    return sum(1 for v in counter.values() if v >= 2)
```

# Counter
- Python의 collections 모듈에서 제공하는 클래스 
- 기본적으로 dictionary를 상속받은 자료구조로 항목의 등장 횟수를 셀 때 사용됨

## 1. 문자열에서 글자 수 세기 


```python
from collections import Counter

s = "hello world"
count = Counter(s)

print(count)
```

    Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})


## 2. 리스트에서 중복된 숫자 세기 


```python
from collections import Counter

nums = [1, 2, 2, 3, 3, 3, 4]
count = Counter(nums)

print(count)
```

    Counter({3: 3, 2: 2, 1: 1, 4: 1})


## 3. 가장 많이 나온 값 찾기(`most_common`)


```python
from collections import Counter

words = ["apple", "banana", "apple", "orange", "banana", "apple"]
count = Counter(words)

print(count.most_common(1)) # 가장 자주 나온 항목 n개를 리스트 형태로 리턴 
```

    [('apple', 3)]


## 4. 두 Counter 객체 간의 합/차 연산 


```python
from collections import Counter

a = Counter("abracadabra")
b = Counter("cadabra")

print(a)
print(b)
print(a + b)
print(a - b)
```

    Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})
    Counter({'a': 3, 'c': 1, 'd': 1, 'b': 1, 'r': 1})
    Counter({'a': 8, 'b': 3, 'r': 3, 'c': 2, 'd': 2})
    Counter({'a': 2, 'b': 1, 'r': 1})


## 5. 조건에 따른 값 필터링 


```python
from collections import Counter

data = Counter("aabbbbccccc")

filtered = {char: count for char, count in data.items() if count >= 2}

print(filtered)
```

    {'a': 2, 'b': 4, 'c': 5}

