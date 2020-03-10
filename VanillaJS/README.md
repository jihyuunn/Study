## JS & DOM
1. document.querySelector('')
    document의 각 태그, id, class를 잡을 수 있다 (body, h1, p 등)
```javascript
let h1 = document.querySelector('h1')
```

1. style.color / style.backgroundColor
    css의 요소를 변경할 수 있다
```javascript
h1.style.color = 'green'
```

1. document.querySelectorAll('')
    document안에 하나의 태그가 보통 여러개 있음
    querySelector로 잡으면 무조건 첫번째 요소만 잡힘
    querySelectorAll로 잡으면 리스트 형태로 모두 잡히고 [0], [1] 등 인덱스 번호로 각각 잡을 수 있다

1. 다른 방법으로 태그나 클래스 잡기
    element's'로 되어 있는건 리스트 형태로 반환되기때문에 [0]선택해줘야 한다
    id는 하나의 document에 하나가 원칙이기 때문에 s가 붙지않는다
```javascript
let id = document.getElementById('idName')
let class = document.getElementsByClassName('className')
let tag = document.getElementsByTagName('tagName')
```

1. button에 function 달기
    onclick에 함수 이름 넣어주고 script에 함수 선언해주면 된다

1. addEventListner
    element.addEventListener(type=이벤트의 종류, listener=이벤트에 따라 수행할 작업)
    공통적인 listener가 사용될 경우 따로 함수로 만든 후에 listener자리에 함수명 집어 넣으면 됨
    - event bubbling 방지: event.stopPropagation() / event.stopImmediatePropagation()
    - stopPropagation() : 위쪽으로 일어나는 이벤트 버블링을 막는다
    - stopImmediatePropagation() : 위쪽 + 현재 요소에 할당된 다른 이벤트까지 막아준다
    예를들어 현재 div를 클릭하면 console.log와 alert 이벤트가 걸려있을 때 stopPropagation을 하면 둘다 실행된다
    버블링을 막아야 하는 경우는 거의 없다

1. innerHTML, outerHTML, textContent
    - innerHTML에는 ''안에 내용이 태그 적용까지 다 된다
    innerHTML은 기존것에 더하는 것이 아니고 새로운 내용으로 덮어쓰기때문에 이미지나 리소스가 새로 불러와진다
    -> 드래그 했던게 풀리고, input안에 내용이 사라지는 등
    - outerHTML은 DOM요소를 수정하지 않는다(개발자도구 elements에는 바뀐 코드가 들어가지만, console에 다시 outerHTML찍어보면 태그는 그대로)
    - textContent는 텍스트만 불러오고 수정하기 때문에 안전하게 사용가능

1. getAttribute('href') / setAttribute('href', 'link')

1. form에서 value가져오기
```HTML
<input id="name" type="text"/>
<label><input type="checkbox" value="라면" name="food"/>라면</label>
<label><input type="checkbox" value="chicken" name="food"/>chicken</label>
<label><input type="checkbox" value="sandwich" name="food"/>sandwich</label>
```
```javascript
let name = document.getElementById('name')
name.value
let foods = document.getElementsByName('food')
btn.addEventListener('click', function() {
    let result = []
    for (let i=0; i<3; i++) {
        let food = foods[i]
        if (food.checked) {
            result.push(food.value)
        }
    }
    alert(result)
})
```