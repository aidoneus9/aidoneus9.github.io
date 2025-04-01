# DOM (Document Object Model) 메소드 및 속성 

```JavaScript
// 선택한다!
document.querySelector(x)
document.querySelectorAll(x)
document.getElementbyId(x)
document.getElementsByClassName(x)
document.write(x) // 문서에 콘텐츠 x를 추가 입력함 

// 확인한다!
Element.textContent
Element.innerText
Element.innerHTML
Element.className
Element.style
Element.title 

```

```JavaScript
let age = parseInt(prompt("age: ")) 

let name = prompt("name: ")
document.write("Murphy" === name) // DOM 단계에서 바꿈 

let name = prompt("이름: ")
document.write(`사용자의 이름은 ${name} <br />`) // DOM 단계에서 바꿈 
document.write(`우리가 찾던 사람인가? ${"Murphy" === name}`) // DOM 단계에서 바꿈
``` 

```JavaScript
const h1 = document.querySelector('h1')
const p = document.querySelector('p')

const isThere = confirm("제목 표시를 할까요?") 
// -> 확인을 누름 
if (isThere) {
    h1.textContent = "문서의 제목"
}

const age = parseInt(prompt("나이가?"))

if (age >= 20) { // else if 추가 가능 
    p.textContent = "1250원" } else {p.textContet = "950원"} 
```

```JavaScript
// 초기, 조건, 반복 
for (let i = 1; i <= 5; i++) {
    document.write(`{i} loading....! <br />`)
}

while (prompt("set number") != 0) {
    document.write("get number! <br />")
}

while (confirm("repeat?")) {}
```

# createElement & appendChild 

```JavaScript
document.createElement() // 지정된 이름의 HTML 요소를 만들어 반환 
document.createElement('div') // 바로 추가 X -> append, appendChild
document.createElement('p')
document.createElement('a')

target.appendChild()

const p = document.createElement('p')
document.body.appendChild(p)

// append: 요소에 노드 객체 또는 문자열을 자식 요소로 추가 (내용만으로도 추가 가능) + 반환 x 
// appendChild: 노드 객체만 추가 (진짜 HTML 태그) + 추가한 자식 노드 반환 

```JavaScript

for (let a = 1; a <= 5; i++) {
    const div = document.getElementById("container")

    const box = document.createElement("div")
    console.log(box)
    box.style.color = "blue" // JavaScript 
    box.style.width = "200px"
    box.style.height = "200px"
    box.textContent = "confusing but still enjoying"

    div.appendChild(box)
}

div.append("text") // 단순 text 추가 가능 
console.log(div.append(box)) // undefined 

```

# 함수 

```JavaScript
// hoisting: 함수 만드는 부분이 호출하는 부분보다 아래에 있어도 된다. 
sayYes()
function sayYes() {} // hoisting O

sayNo() // X 
const sayNo = function() {} // hoisting X 

function createParagraph() {
    const p = document.createElement("p")
    p.style.color = "red" // <- argument 
    p.textContent = "new paragraph!" // <- argument 
    document.querySelector("#container").append(p)
}
```

## 이벤트 핸들링 

```JavaScript 
// Event: DOM에서 발생하는 다양한 액션 또는 상호작용 동작을 나타내는 프로그래밍 인터페이스 

const handleClick = function(){
    window.alert("welcome!")
}

const button = document.querySelector("button")

button.onclick = handlieClick // <- ⭐️ on___
```

### addEventListener(이벤트명, 이벤트 핸들러)

```JavaScript 
spanBtn.onclick = function() {
    const span = document.createElement("span")
    span.textcontent = "new span tag"
    document.body.append(span)
}
// -> 아래와 같이 바뀜 
spanBtn.addEventListener("click", function(){
    const span = document.createElement("span")
    span.textcontent = "new span tag"
    document.body.append(span)
})

```

```JavaScript 
const spanBtn = document.getElementById("span")
const strongBtn = document.getElementById("strong")
const markBtn = document.getElementById("mark")

const handleClick = function(event) {
    if (evenet.target.id == "span") {
        const span = document.createElement("span")
        span.textContent = "new span tag"
        document.body.append(span)
    }
    else if (evenet.target.id == "strong") {
        const strong = document.createElement("strong")
        strong.textContent = "new strong tag"
        document.body.append(strong)
    }if (evenet.target.id == "mark") {
        const mark = document.createElement("mark")
        mark.textContent = "new mark tag"
        document.body.append(mark)
    }
}

spanBtn.addEventListner("click", handleClick)
strongBtn.addEventListner("click", handleClick)
markBtn.addEventListner("click", handleClick)


```

### 입력 요소로부터 값 읽어들이기

- textContent: 요소에 쓰인 텍스트에 접근 
- value: 사용자가 직접 요소에 입력한 값에 접근 (rw)

```HTML
<!-- <form> -->
<form>
    <input name = "이름" />
    <input name = "별명" />
    <input type = "submit" />
<form>
```

-> name 속성값을 토대로 입력값에 접근 

```JavaScript
const form = document.querySelector("form")
form.addEventListener("submit", function(e) {
    console.log(e.target.이름.value)
    console.log(e.target.별명.value)
})
```

```JavaScript
const input = document.getElementById("talk")
const button = document.getElementById("push")

input.addEventListener("keyup", function(e) {
    console.log(e.target.value)
})

button.addEventListener("click", function() {
    const p = document.createElement("p")
    p.textContent = input.value
    document.body.append(p)
}
```

```JavaScript

const form = document.getElementById("form")
form.addEventListener("submit", function(event) {
    event.preventDefault() // 제출 발생 시 새로 고침 안 함. 
    const p = document.createElement("p")
    p.textContent = `${event.target.name.value}의 별명은 ${event.target.nick.value}`
})

```


