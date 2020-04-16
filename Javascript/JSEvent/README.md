### HTML속성과 DOM프로퍼티를 이용한 Event Handler 할당
```javascript
<button id="click" onclick="alert('clicked')" value="click">
<script>
    click.onclick = function() {
        alert('hello')
    }
</script>
```
- HTML 태그 안에 onclick에 값을 할당하여 이벤트를 더해줄 수 있다
- 스크립트 안에서 클릭 이벤트를 할당해줄 수 있다
- 위와 같이 클릭 이벤트를 두개 할당 시 기존 핸들러는 덮어씌워진다   

```javascript
button.onclick = saySomething; //1
button.onclick = saySomething(); //2
<button id="button" onclick="saySomething()"> //3
button.onclick = function() {
    saySomething();
} //3번의 핸들러함수
```
두번째 방법은 틀린 방법, 왜냐하면 saySomething()으로 호출시에 return된 값이 할당된다   
그런데 태그 안에서는 괄호가 포함된 함수를 넣어야한다, 왜냐하면 브라우저는 속성값을 읽고 이 값을 함수 본문으로 하는 핸들러 함수를 만들기 때문   

### addEventHandler
HTML 속성과 DOM 프로퍼티를 이용한 이벤트 핸들러 할당 방식으로는 하나의 이벤트에 복수의 핸들러를 할당할 수 없다(덮어씌워진다)   
```javascript
element.addEventListener(event, handler[, options]);
```
- event 이벤트 이름(onclick, keypress 등)
- handler 핸들러 함수, 실제 함수
- options 아래 프로퍼티를 갖는 객체
삭제하고 싶을 때는 removeEventListener로 하고 동일한 함수만 삭제 가능하다   

*이벤트가 발생하면 브라우저는 이벤트객체라는 것을 만들고, 여기에 이벤트 관련 상세한 정보를 넣은 후 핸들러 함수에 인수형태로 전달한다*   
e.g. eventType 클릭이나, 키프레스 등   
객체나 클래스를 이벤트 핸들러로 할당할 수 있다   

### Event Bubbling
한 요소에 이벤트가 발생하면 그 요소의 부모 요소 핸들러까지 실행이 되는 것, document 객체를 만날때까지 이 과정이 반복된다   
FORM > DIV > P 일때 P태그를 누르면 DIV, FORM에 있는 핸들러가 모두 실행된다   
event.target으로 이벤트 시작 태그를 알 수 있다   
event.stopPropagation() : 위쪽으로 일어나는 이벤트 버블링을 막아준다   
event.stopImmediatePropagation() : 버블링도 멈추고, 요소에 할당된 다른 핸들러까지 막아줌   

_그러나 이벤트 버블링을 막아야하는 경우는 거의 없다_

### Event Capturing
이벤트가 하위요소에 전달되는 것, 캡쳐링 단계를 이용해야하는 경우는 거의 없다   
```javascript
element.addEventListener('event', handler, true);
// option을 true로 하면 캡쳐링이 일어난다
```

### Event Delegation
캡쳐링과 버블링을 이용해 강력한 이벤트 핸들링 패턴인 이벤트 위임을 구현할 수 있다   
비슷한 방식으로 여러 요소를 다뤄야 할 때 사용되고, 요소의 공통 조상에 이벤트 핸들러를 하나만 할당해도 여러요소를 한꺼번에 다룰 수 있다
```javascript
let selectedId;
//테이블 안에 있는 곳을 아무데나 눌렀을 때 태그 네임이 'TD'가 아니면 아무런 효과가 나지않고
//태그네임이 'TD'이면 hightlight 함수가 실행이 된다 -> 클래스 추가 됨
table.onclick = fuction(event) {
    let target = event.target;
    if (target.tagName != 'TD') return;
    highlight(target); 
}
function highlight(td) {
    if (selectedId) {
        selectedId.classList.remove('highlight');
    }
    selectedId = td;
    selectedId.classList.add('highlight');
}
```   