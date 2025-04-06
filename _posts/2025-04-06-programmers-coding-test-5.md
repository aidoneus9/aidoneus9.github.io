# for에 변수가 세 개일 경우  

## 1. zip()을 이용하여 여러 리스트를 동시에 순회할 때 

```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = [True ,False, True]

for x, y, z in zip(list1, list2, list3):
    print(x, y, z)

# 출력 
1 a True
2 b False
3 c True
```

## 2. 튜플을 반환하는 이터러블을 순회 

```python
data = [(1, 'apple', 3.5), (2, 'banana', 2.0), (3, 'cherry', 5.0)]

for num, fruit, price in data:
    print(num, fruit, price)

# 출력
1, apple, 3.5
2, banana, 2.0
3, cherry, 5.0 
```
