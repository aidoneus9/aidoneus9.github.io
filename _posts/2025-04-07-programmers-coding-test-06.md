---
layout: single
title: 코딩테스트 암기사항 5.
---

```python
def solution(arr, queries):
    answer = []
    # 쿼리에 맞는 서브리스트 추출 
    for i in queries:
        sublist = arr[i[0]:i[1] + 1]
        
        # ⚠️ 거르기
        filtered = list(filter(lambda x: x > i[2], sublist))
        
        # ⚠️ 거른 것 중 최솟값 
        if filtered: 
            answer.append(min(filtered))
        
        # ⚠️ 걸러진 게 없으면 
        else:
            answer.append(-1)
            
    return answer
```


```python
def solution(rank, attendance):
    # ⭐️ 중요
    present =[(r, i) for i, (r, a) in enumerate(zip(rank, attendance)) if a] 
    # -> [(3, 0), (2, 2)]를 sorted로 정렬 시 각 튜플의 첫 번째 원소가 기준이 됨 

    top3 = sorted(present)[:3]
    
    # 각 인덱스를 가져옴
    i, j, k = top3[0][1], top3[1][1], top3[2][1]
    
    return 10000 * i + 100 * j + k
```


```python
number = int(input())

answer = 0

while number != 0: # 몫이 0이 될 때까지
    answer += number % 100
    number //= 100

print(answer)
```


```python
from collections import Counter

def solution(array):
    counter = Counter(array) # 각 요소의 개수를 세는 딕셔너리 {1: 2, 2: 3, 3: 1}
    most_common = counter.most_common() # value 기준으로 내림차순 정렬된 리스트 반환 [(2, 3), (1, 2), (3, 1)]
    
    if len(most_common) == 1 or most_common[0][1] != most_common[1][1]:
        return most_common[0][0]
    else:
        return -1
```


```python
# 다항식 더하기 

def solution(polynomial):
    x_sum = 0
    num_sum = 0
    
    for term in polynomial.split(" + "):
        if "x" in term:
            x_sum += int(term[:-1]) if term != "x" else 1
        else:
            num_sum += int(term)
        
    answer = []    
    if x_sum:
        answer.append(f'{x_sum}x' if x_sum > 1 else "x")
    if num_sum:
        answer.append(str(num_sum))
        
    return ' + '.join(answer) if answer else "0"
```


```python
def solution(common):    
    a, b, c = common[:3] # ✅ 동시 변수 할당
    if b - a == c - b:
        diff = b - a
        return common[-1] + diff 
    
    else:
        ratio = b / a
        return common[-1] * ratio
```


```python
'''
def solution(participant, completion):            
    # count(n) -> 시간복잡도 O(n) 
    for par in participant: # n
        if participant.count(par) != completion.count(par): # n x 2 => 총 n x n x 2의 시간복잡도를 가지게 됨 
                return par  
'''         
from collections import Counter

def solution(participant, completion):       
    answer = Counter(participant) - Counter(completion)
    return list(answer.keys())[0]

```
