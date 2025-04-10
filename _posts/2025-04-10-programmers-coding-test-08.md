---
layout: single
title: 코딩테스트 암기사항 7.
---

```python
# 문자열 -> 뒤집기 -> find (여러 문자열 가능)
# == rfind (마지막 부분의 시작 인덱스)
'''
# 방법 1. find 
def solution(myString, pat):
    reversedString = myString[::-1] # "GFEdCbA"
    reversedPat = pat[::-1] # "Ed"
    
    reversedAnswer = reversedString[reversedString.find(reversedPat):]
    
    return reversedAnswer[::-1]
'''
# ✏️ 방법 2. rfind
def solution(myString, pat):
    idx = myString.rfind(pat)
    
    return myString[:idx + len(pat)]
```


```python
'''
def solution(quiz):
    # 배열에 속한 각 수식마다 -= 또는 +=로 분리함
    answer = []
    for i in range(len(quiz)):
        quiz[i] = quiz[i].split(" ") # [["3","-","4","=","-3"],["5","+","6","=","11"]]
       
        if "-" in quiz[i]:
            if int(quiz[i][0]) - int(quiz[i][2]) == int(quiz[i][4]):
                answer.append("O")
            else:
                answer.append("X")
                
        elif "+" in quiz[i]:
            if int(quiz[i][0]) + int(quiz[i][2]) == int(quiz[i][4]):
                answer.append("O")
            else:
                answer.append("X")
                
    return answer
'''
def solution(quiz):
    answer = []
    
    for q in quiz:
        left, _, right = q.partition("=") # ✏️ partition: 항상 세 개의 결과를 튜플로 줌 (앞쪽, 구분자, 뒷쪽)
        if eval(left.strip()) == int(right): # ✏️ eval: 문자열로 된 파이썬 코드를 실제 코드처럼 계산해주는 함수 -> ⚠️ 사용자 입력을 eval로 직접 실행할 경우 매우 위험 (보안)
            answer.append("O")
        else:
            answer.append("X")
            
    return answer
```


```python
def solution(answers):
    # 1. 찍기 패턴 배열 안에 넣기 ✏️
    patterns = [[1, 2, 3, 4, 5], [2, 1, 2, 3, 2, 4, 2, 5], [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]] 
    
    
    scores = []
    for pattern in patterns:
        # 2. 답안 배열 생성 
        full =  pattern * (len(answers) // len(pattern)) + pattern[:len(answers) % len(pattern)]
        # 3. 각 답안마다 answers와 비교, 정답 개수 
        correct = sum([1 for i, ans in enumerate(answers) if full[i] == ans])
        scores.append(correct)
        
    # 4. 가장 많이 맞힌 사람(들) 리턴     
    max_score = max(scores)
    return [i + 1 for i, score in enumerate(scores) if score == max_score] 
```
