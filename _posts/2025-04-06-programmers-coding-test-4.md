---
layout: single
title: 코딩테스트 암기사항 3. 
---

```python
def solution(my_string):
    alphabet = [chr(i) for i in range(ord('A'), ord('Z') + 1)] + [chr(i) for i in range(ord('a'), ord('z') + 1)]
    
    counts = [my_string.count(char) for char in alphabet]
        
    return counts
```


```python
def solution(bin1, bin2):
    # 십진수로 바꾼 다음 -> 이진수로 바꾸기(파이썬 내장함수 이용)
    
    # 1. 십진수로 바꾸고 합 구하기
    add = int(bin1, 2) + int(bin2, 2)
    # 2. 이진수로 바꾸기 bin(정수) -> 이진수 문자열로 반환 
    return bin(add)[2:]

```


```python
def solution(arr):
    stk = []
    for num in arr:
        if stk and stk[-1] == num:
            stk.pop()
        else:
            stk.append(num)
         
    return stk or [-1] # ⭐️
```


```python
def solution(arr):
    stk = []
    i = 0
    while(i < len(arr)):
        if not stk or stk[-1] < arr[i]:
            stk.append(arr[i])
            i += 1 # <- 여기는 있고 
        else:
            stk.pop() 
            # ⚠️ 여긴 없음 -> 그래서 while문을 썼음 
           
    return stk
```


```python
# def solution(food):
#     # food = [1, 7 ,1, 2] -> 유효한 것은 1번 인덱스부터임 
#     left = ""
#     for i in range(1, len(food)):
#         q, _ = divmod(food[i], 2)
#         left += q * str(i)
     
#     return left + "0" + left[::-1]

# ✅ 리스트에 모아서 join하는 방식이 += 보다 성능이 좋고 깔끔함  
def solution(food):
    left = []
    for i in range(1, len(food)):
        left.append(str(i) * (food[i] // 2))  # 반씩 나눠서 추가

    left_str = ''.join(left)
    return left_str + '0' + left_str[::-1]
```


```python
# def solution(k, score):
#     answer = []
#     # score 중에서 처음 k개를 append
#     pride = []
#     for i in range(min(k, len(score))): # <- ✅ 예외 사례: min(k, len(score))
#         pride.append(score[i])
#         answer.append(min(pride))
        
#     # score의 k+1번째 수와 min(pride) 비교해서 그보다 크면 replace
#     for i in range(k, len(score)):
#         if min(pride) < score[i]:
#             pride[pride.index(min(pride))] = score[i]
#             answer.append(min(pride))
#         else: 
#             answer.append(min(pride))
            
#     return answer 

# ✅ heapq
import heapq # 항상 가장 작은 값이 맨 앞에 오도록 자동 정렬되는 리스트를 만들어 줌

def solution(k, score):
    # 초기 설정 
    answer = []
    hall = []
    
    for s in score: 
        heapq.heappush(hall, s) # hall에 s 추가하면서 자동 정렬
        if len(hall) > k:
            heapq.heappop(hall) # hall에서 가장 작은 값을 꺼냄 -> 계속 k개의 수를 유지
        answer.append(hall[0])
    
    return answer   
    
```


```python
def solution(ineq, eq, n, m):
#     if n < m and (ineq == "<" and (eq == "=" or eq == "!")):
#         return 1 
        
#     elif n == m and ((ineq == "<" or ineq == ">") and (eq == "=")):
#         return 1

#     elif n > m and (ineq == ">" and (eq == "=" or eq == "!")):
#         return 1
    
#     return 0
    op = ineq + eq # ✅ 발상 
    
    if op == "<=":
        return int(n <= m) # ✅ int(True)는 1을, int(False)는 0
        
    elif op == "<!":
        return int(n < m)
    
    elif op == ">=":
        return int(n >= m)
    
    elif op == ">!":
        return int(n > m)

```


```python
def solution(numbers, k):
    # 0번 인덱스부터 2씩 건너뛰며 k번째 사람을 찾는 것. (<- 이런 식으로 써보기)
    return numbers[2 * (k - 1) % len(numbers)]
```


```python
def solution(id_pw, db):
    for arr in db:
        if id_pw[0] == arr[0]:
            if id_pw[1] == arr[1]:
                return "login"
            else:
                return "wrong pw"
    return "fail" # ✅ 반복문을 다 돌았는데도 아이디가 없음 
```


```python
def solution(my_string, queries):
    for start, end in queries: # unpacking
        my_string = my_string[:start] + my_string[start:end + 1][::-1] + my_string[end + 1:]
        
    return my_string 
```


```python
'''
def solution(arr, k):
    random = list(dict.fromkeys(arr)) # ✅ dict.fromkeys(arr) 순서를 지키고 중복을 제거 
    # list(set(arr)) <- ⚠️ 순서가 보장되지 않음. 그래서 틀렸어
    
    return random[:k] if len(random) >= k else random + [-1] * (k - len(random))
'''    

def solution(arr, k):
    unique = list(dict.fromkeys(arr))
    padding = [-1] * (k - len(unique))

    return unique[:k] + padding
```


```python
# 방법 1. 
# def solution(spell, dic):
#     for word in dic:
#         if ''.join(sorted(''.join(spell))) in ''.join(sorted(word)):
#             return 1 
        
#     return 2

# ⚠️ sorted 하면 list로 반환됨 

# 방법 2-1. set, any 이용 
def solution(spell, dic):
    if any(set(spell) == set(word) for word in dic):
        return 1
    return 2

# 방법 2-2. for문 이용 (성능 차이 없음)
# def solution(spell, dic):
#     for word in dic:
#         if set(spell) == set(word):
#           return 1
#     return 2
```


```python
# 방법 1. swapcase()
str = input()
print(str.swapcase())

# 방법2. islower(), isupper() 
```


```python
'''
def solution(chicken): 
    q, r = divmod(chicken, 10)
    eat = q 
    while((q + r) >= 10):
        q, r = divmod(q + r, 10) 
        eat += q
    return eat
'''
def solution(chicken):
    coupons = chicken
    services = 0
    
    while coupons >= 10:
        free = coupons // 10 
        services += free 
        coupons = coupons % 10 + free 
        
    return services 
```


```python
def solution(s):
    # 생각나는 예외들을 걸렀음
    if s.count(")") != s.count("(") or s.startswith(")") or s.endswith("("):
        return False
    
    '''
    # 괄호 외 문자를 걸렀음 -> 밑의 코드로 이 역할 가능 
    stack = []
    for char in s:
        if char == "(" or char == ")":
            stack.append(char)
    '''
    
    # 🤔 왜 이 코드만 쓰면 안되는 걸까? -> 배열에 값이 없는데 pop을 쓸 경우 오류가 나기 때문 
    mars = []
    for char in s:
        if char == "(":
            mars.append(char)
        elif char == ")":
            if mars:
                mars.pop()
                
    return len(mars) == 0    
```
