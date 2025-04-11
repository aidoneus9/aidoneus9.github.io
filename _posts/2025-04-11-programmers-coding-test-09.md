```python
# ✏️ RegEx 사용
'''
import re 

def solution(babbling):
    count = 0
    for s in babbling:
        if re.fullmatch(r'(aya|ye|woo|ma)+', s) is not None:
            count += 1
    return count
'''

import re

def solution(babbling):
    valid_pattern = re.compile(r'^(aya|ye|woo|ma)+$')
    return sum(1 for word in babbling if valid_pattern.fullmatch(word))
```

# 정규표현식(RegEx)
- 문자열에서 특정한 패턴을 찾기 위한 도구  
- 어떤 문자열이 내가 원하는 형식에 맞는지 검사하거나, 그 중에서 필요한 부분만 뽑아낼 수 있는 도구 

### ✏️ 기초 문법 요약 
| 패턴 | 의미 | 예시 |
|:---:|:---:|:---:|
|`.`|아무 글자 한 개|`a.b` -> `"acb"`, `"a7b"` 등 가능|
|`\d`|숫자(digit)|`\d\d\d` -> `123`|
|`\D`|숫자 아닌 것|`\D+` -> `"abc"`, `"가나다"`|
|`\w`|알파벳/숫자/밑줄 `[a-zA-Z0-9_]`|`\w+` -> `"hello"`, `"test_123"`|
|`\W`|`\w`의 반대(특수문자 등)|`\W+` -> `"!"`, `"@"`, `"*"`|
|`\s`|공백 문자(space, tab, 개행 등)|`\s+` -> `" "`|
|`\S`|공백 아닌 것|`\S+` -> `"hello"`|
|`+`|앞 문자가 한 번 이상 반복|`a+` -> `a`, `aa`, `aaa`|
|`*`|앞 문자가 0번 이상 반복|`a*` -> `''`, `a`, `aa`, `aaa`|
|`?`|앞 문자가 0번 또는 한 번|`a?` -> `''`, `a`|
|{n}|정확히 n번 반복|\d{4} -> `"2024"`|
|{n,}|n번 이상 반복|a{2,} -> `"aa"`, `"aaa"`|
|{n, m}|n ~ m번 반복|a{2, 4} -> `"aa"`, `"aaa"`, `"aaaa"`|
|`[]`|문자 집합(괄호 안 하나와 매치)|`[abc]` -> `"a"`, `"b"`, `"c"` 중 하나|
|`[^abc]`|a, b, c를 제외한 문자|`"d"`, `"z"` 등|
|`[0-9]`|숫자|`"3"`|
|`[a-z]`|소문자|`"m"`|
|`[A-Z]`|대문자|`"Q"`|
|`[가-힣]`|한글 완성형 문자|`"가"`, `"힣"`등|
|`^`|문자열 시작|`^a` -> a로 시작|
|`$`|문자열 끝|`z$` -> z로 끝| 
|그 외 하단 예시|||


```python
# 휴대폰 번호 찾기
import re

text = "제 번호는 010-1234-5678 입니다."
pattern = r'\d{3}-\d{4}-\d{4}'

re.search(pattern, text).group()
# re.search(...) -> 찾아줘
# .group() -> 찾은 거 보여줘

# 이메일 찾기
text = "제 메일 주소는 hello@world.com 입니다."
pattern = r'\w+@\w+\.\w+'

re.search(pattern, text).group()
```

##### `(abc)`
- 괄호 ()를 사용하면 하나의 덩어리로 인식
- 반복하거나 순서를 제어할 때 유용
```Python
import re

text = "hahaha"
re.search(r'(ha)+', text).group() # 'hahaha'
# (ha)+는 "ha"라는 묶음을 반복해서 찾음
# -> "ha", "haha", "hahaha" 모두 매치됨
```

##### `a|b` 
- or 연산자
```Python
re.search(r'cat|dog', 'I have a cat').group() # 'cat'
# "cat" 또는 "dog" 중 하나라도 있으면 매치됨
```

##### `(?:abc)`
- 일반 `(abc)`는 그룹을 만든 후 결과에서 꺼내 쓸 수 있음 -> `(?:abc)`는 그룹은 필요하지만 굳이 결과로 꺼내 쓰진 않을 때 씀
- 성능이 미세하게 좋아지고, 복잡한 정규식에서 실수를 줄임
```Python
text = "abcabc"
re.findall(r'(abc)', text) # ['abc', 'abc']
re.findall(r'(?:abc)', text) # ['abc', 'abc']
```

##### `(?P<name>abc)`
- `(abc)`같은 그룹에 이름을 붙여서 꺼내 쓰는 방식
- 더 복잡한 정규식에서도 가독성과 명확성이 생김
```Python
text = "이름: 가나디"
match = re.search(r'이름:\s*(?P<name>[가-힣]+)', text)
print(match.group('name')) # '가나디'
# (?P<name>[가-힣]+)에서 한글 이름 부분에 name이라는 이름을 줘서 group('name')으로 꺼냄
``` 

# re 모듈
- Python에서 RegEx를 쓸 수 있게 해주는 도구 

|함수|설명|
|---:|:---|
|`re.search(pattern, string)`|처음 등장하는 패턴을 찾아서 매치 객체 반환|
|`re.match(pattern, string)`|문자열의 시작부터 패턴이 매치되는지 검사|
|`re.fullmatch(pattern, string)`|문자열 전체가 패턴에 완벽하게 매치되는지 검사|
|`re.findall(pattern, string)`|패턴에 매치되는 모든 부분 문자열을 리스트로 반환|
|`re.finditer(pattern, string)`|매치되는 모든 결과를 이터레이터로 반환(하나씩 탐색 가능)|
|`re.sub(pattern, repl, string)`|패턴을 찾아서 `repl`로 치환(replace)|
|`re.split(pattern,string)`|패턴을 기준으로 문자열 쪼개기|
|`re.compile(pattern)`|패턴을 미리 컴파일해서 성능 향상(반복해서 쓸 때 유리)|


```python
import re

text = "고양이가 가나디와 놀고 있다."

# search
re.search(r'가나디', text).group() # '가나디'
# -> text안에서 '가나디'라는 패턴을 처음으로 찾음

# match
re.match(r'고양이', text).group() # '고양이'
# -> 문자열 '처음부터' 패턴이 맞는지 확인: 이 경우 text가 '고양이가...'로 시작하므로 패턴 '고양이'와 매치됨

# fullmatch
re.fullmatch(r'.+', text).group() # '고양이가 가나디와 놀고 있다.'
# .+가 한 글자 이상 모든 문자라는 뜻이므로, 전체 문장이 매치됨 

# findall
re.findall(r'[가-힣]+', text) # ['고양이가', '가나디와', '놀고', '있다']
# [가-힣]+는 한글로 이루어진 단어들을 찾아줌

# finditer
for m in re.finditer(r'[가-힣]+', text):
    print(m.group())
# 고양이와
# 가나디가
# 놀고
# 있다
# finditer()는 findall과 비슷하지만 반복자로 결과를 줌. 

# sub
re.sub(r'고양이', '토끼', text) #토끼가 가나디와 놀고 있다. 
# '고양이'라는 패턴을 찾아서 '토끼'로 치환

# split
re.split(r'\s+', text) # 공백 기준 분리 = ['고양이가', '가나디와', '놀고', '있다.']
# split은 패턴을 기준으로 문자열을 쪼갬
# \s+는 공백(스페이스, 탭 등) 하나 이상을 뜻함 

# compile
pattern = re.compile(r'가나디')
pattern.search(text).group() # '가나디'
# compile()은 정규식 패턴을 미리 만들어 놓는 것으로 패턴을 여러 번 사용할 경우 성능이나 가독성에서 유리함
```
