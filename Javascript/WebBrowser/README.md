# 웹 브라우저에서의 입출력   

### 이벤트 처리기와 타이머   
- 이벤트 처리기: 이벤트가 발생했을 때 실행되는 함수   
함수를 이벤트 처리기로 등록하는 방법은 세 가지이다   
1. HTML 요소의 속성으로 등록하는 방법
```HTML
<script>
    function displayTime() {
        const d = new Date();
        console.log(d.toLocaleString())
    }
</script>
<button onclick="displayTime()">click</button>
<!-- onmouseup, onmousedown, onsubmit 등 다양한 이벤트 유형이 가능하다 -->
```
이벤트 처리기 속성을 사용해서 이벤트 처리기 등록을 하면 HTML코드와 자바스크립트 코드가 뒤섞이는 단점이 있다. 분리하려면 DOM, addEventListener를 사용하면 된다    

2. DOM에서 가져온 HTML요소에 이벤트 처리기 지정하기   
- DOM: 자바스크립트 등 프로그램이 HTML요소를 조작할 수 있게 하는 인터페이스   
DOM객체(window, document, 요소)로 HTML 문서를 조작한다, HTML코드와 자바스크립트 코드를 분리할 수 있다 -> 가독성과 유지보수성이 높아짐    
```HTML
<script>
    function displayTime() {
            const d = new Date();
            console.log(d.toLocaleString())
        }
    window.onload = function() {
    // 이 코드로 HTML 문서를 모두 읽어들인 후 우변의 함수를 실행시킬 수 있다(원래는 HTML문서를 해석하는 도중에 script요소를 발견하면 코드를 실행한 다음에 HTML을 다시 해석한다)
        const button = document.getElementById('button');
        button.onclick = displayTime;
    }
</script>
<button id="button">click</button>
```
HTML문서를 모두 읽어들인 후에 특정 id 속성값을 가진 HTML요소의 요소객체를 가져오고, 이벤트 처리기 프로퍼티(onclick)에 이벤트 처리기로 동작할 함수(displayTime)를 등록한다    
모든 요소 객체에는 이벤트 처리기 프로퍼티가 마련되어 있다(onkeydown:null, onkeyup:null, onclick: displayTime 등등...)    

### 타이머   
- setTimeOut: 지정된 시간이 흐른 후에 함수 실행   
- setInterval: 지정된 시간마다 반복해서 함수 실행   

### HTML요소 읽고 쓰기   
- innerHTML: HTML요소의 내용을 읽거나 쓸 수 있다    
- input type=number, text: value(입력값을 문자열로 변환한 값)    
- input type=checkbox, radio: checked(선택 여부를 뜻하는 논리값)    
- select: selectedIndex(선택된 option 요소를 가리키는 0부터 시작하는 번호)   
- textarea: value   
```HTML
<script>
    window.onload = function() {
        const button = document.getElementById('button');
        button.onclick = function() {
            const height = parseFloat(document.getElementById('height').value);
            const weight = parseFloat(document.getElementById('weight').value);
            const bmi = document.getElementById('bmi');
            bmi.innerHTML = (weight/height/height)
        }
    }
</script>
<input type="number" id="height" />
<input type="number" id="weight" />
<input type="button" value="click" id="button" />
<p id='bmi'></p>
```

### Canvas
- Canvas로 2차원 그래픽과 WebGL을 사용한 3차원 그래픽을 구현할 수 있다   
