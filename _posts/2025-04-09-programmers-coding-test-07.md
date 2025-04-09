---
layout: single
title: 코딩테스트 암기사항 6.
---

```python
def solution(picture, k):
    result = []
    for row in picture: # 각 행에 대해서
        expanded_row = ''.join(char * k for char in row) # <- 한 줄로 작성 
        # 그 행 자체도 k번 반복 
        for _ in range(k): # <- # k번 반복에 대해 
            result.append(expanded_row)
    return result 
```


```python
def solution(num, total):
    # 중간값 기준으로 구하기
    q, r = divmod(total, num)
    answer = []
    
    # 1. 중간값이 있을 때 
    if r == 0: # q가 중간이 되고 개수는 num개 
        for i in range(q - ((num - 1) // 2), q + ((num - 1) // 2) + 1): # <- ⚠️ 이 코드 상에서 //가 아닌 /를 쓰면 TypeError: 'float' object cannot be interpreted as an integer가 남 
            answer.append(i)
    # 2. 중간값 없을 때        
    if r != 0: # q가 중간 왼쪽 값이 되고 개수는 num개 
        for i in range(q - ((num - 2) // 2), q + num // 2 + 1):
            answer.append(i)
            
    return answer
```


```python
'''
def solution(n):
    not_three = []
    # 개수가 n개가 될 때까지 1번부터 리스트를 만들고, 리스트[-1]을 함 
    i = 1   
    while True:
        if i % 3 != 0 and "3" not in str(i):
            not_three.append(i)
            if len(not_three) == n:
                break
        i += 1    
    return not_three[-1]
'''        
def solution(n):
    count = 0 # ✅ 불필요한 리스트를 만들지 않음 -> 메모리 효율 
    i = 1
    while True:
        if i % 3 != 0 and "3" not in str(i):
            count += 1
            if count == n:
                return i     
        i += 1
```


```python
import math
def solution(a, b):
    gcd = math.gcd(a, b)
    b //= gcd 
    
    # ✏️ 아이디어: b를 2, 5로 계속 나눠서 1이 되면 b의 소인수는 2와 5뿐임. 
    for p in [2, 5]: # [2, 5]에 있는 2, 5를 하나씩 꺼내서 순서대로 p에 넣는다
        while b % p == 0:
            b //= p 
            
    return 1 if b == 1 else 2
```


```python
def solution(A, B):
    for i in range(len(A)):
        if A == B:
            return i
        A = A[-1] + A[:-1]
    return -1
```


```python
'''
def solution(l, r):
    answer = []
    for i in range(l, r + 1):
        if all(c in ["0", "5"] for c in str(i)): # ✅
            answer.append(int(i)) 
    return sorted(answer) if answer else [-1]
'''
def solution(l, r):
    answer = [i for i in range(l, r + 1) if set(str(i)) <= {"0", "5"}] # ✅
    return answer if answer else [-1]
```


```python
'''
def solution(numlist, n):
    # 기준 숫자와의 차를 구해서 딕셔너리로 저장 {원래 값: 차}
    diff = []
    for num in numlist:
        diff.append(abs(n - num))
    harry = dict(zip(numlist, diff))
    
    # 오름차순 정렬 & 단, 값이 같을 경우 키 값이 더 큰 수가 앞에 오도록 배치 
    ron = dict(sorted(harry.items(), key=lambda x: (x[1], -x[0]))) # ✅
                         
    # 키 값만 뽑아내기 
    return list(ron.keys()) ✅ list로 씌워줄 것    
'''
# 딕셔너리를 쓰지 않는 방법 
def solution(numlist, n):
    return sorted(numlist, key=lambda x: (abs(n - x), -x))
```


```python
def solution(code):
    ret = ""
    mode = 0
    for index, char in enumerate(code):
        # mode가 바뀌는 조건 
        if char == "1":
            mode = 1 - mode
            continue # 1을 처리한 다음에는 뒤의 조건이 무의미함 
            
        if (mode == 0 and index % 2 == 0) or (mode == 1 and index % 2 != 0): 
            ret += code[index]
                
    return ret if ret else "EMPTY" 
            
```


```python
def solution(array, n):
    return min(array, key=lambda x: (abs(x - n), x)) # min의 정렬 기준 주기 
    
```


```python
def solution(keyinput, board):
    x, y = 0, 0
    max_x = (board[0] - 1) // 2
    max_y = (board[1] - 1) // 2 
    
    move = {
        "right": (1, 0),
        "left": (-1, 0),
        "up": (0, 1),
        "down": (0, -1)
    } # ✅ 딕셔너리와 튜플 형태로 저장 

    for key in keyinput: 
        dx, dy = move[key] # ✅ 
        x = max(-max_x, min(max_x, x + dx)) # 😬
        y = max(-max_y, min(max_y, y + dy)) # 😬
        
    return [x, y]

```
