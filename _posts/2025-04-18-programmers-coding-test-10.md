---
layout: single
title: 코딩테스트 암기사항 9.
---

```python
def solution(score):
    # 평균 점수 구하기 
    avg_with_index = [(i, (s[0] + s[1]) / 2) for i, s in enumerate(score)]
    # -> [(0, 75.0), (1, 75.0), (2, 40.0), (3, 95.0), (4, 95.0), (5, 100.0), (6, 20.0)]
    
    # 내림차순 정렬 
    sorted_avg = sorted(avg_with_index, key=lambda x: -x[1])
    # -> [(5, 100.0), (3, 95.0), (4, 95.0), (0, 75.0), (1, 75.0), (2, 40.0), (6, 20.0)]
    
    # 등수 매기기 (공동 순위 처리)
    rank_dict = {}
    rank = 1
    for (idx, avg) in sorted_avg:
        if avg not in rank_dict:
            rank_dict[avg] = rank
        rank += 1

    # 최종 정답: 원래 순서대로 등수 반환
    return [rank_dict[(s[0] + s[1]) / 2] for s in score]
```


```python
# 🧭 8방향 델타 탐색 
def solution(board):
    n = len(board)
    danger = [[0] * n for _ in range(n)] 
    
    # 8방향 델타 
    dx = [-1, -1, -1, 0, 0, 1, 1, 1]
    dy = [-1, 0, 1, -1, 1, -1, 0, 1]
    
    for i in range(n):
        for j in range(n):
            if board[i][j] == 1:
                danger[i][j] = 1
                for d in range(8):
                    ni, nj = i + dx[d], j + dy[d]
                    if 0 <= ni < n and 0 <= nj < n:
                        danger[ni][nj] = 1
                        
    safe_count = 0
    for i in range(n):
        for j in range(n):
            if danger[i][j] == 0:
                safe_count += 1
    
    return safe_count
```


```python
from collections import Counter

def solution(a, b, c, d):
    count = Counter([a, b, c, d]) # <- ✅dict 씌우지 않고 그대로 사용 가능
    
    if len(count) == 1:
        p = next(iter(count))
        return 1111 * p
    
    if len(count) == 2 and 3 in count.values():
        p, q = [item[0] for item in sorted(count.items(), key=lambda x: -x[1])]
        # count.items() -> (key, value) 쌍의 튜플들  
        return (10 * p + q) ** 2
    
    if len(count) == 2 and list(count.values()) == [2, 2]:
        p, q = count.keys()
        return (p + q) * abs(p - q)
    
    if len(count) == 3:
        q, r = [key for key, value in count.items() if value == 1]
        return q * r
    
    return min(count)
```
