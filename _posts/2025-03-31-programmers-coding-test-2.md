### 암기 사항 

🚀 소수 판별 함수 


```python
def is_prime(n):
    if n <= 1:
        return False
    # 소수 판별 최적화: n이 2 이상인 홀수만 판별  
    if n == 2:
        return True
    if n % 2 == 0:
        return False
    
    for i in range(3, int(n**0.5) + 1, 2):
        if n % i == 0:
            return False 
    return True 
```
