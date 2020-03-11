### Closure
클로져는 함수 바깥의 변수들을 기억하고 접근할 수 있는 함수를 말한다

### nested function
함수 안에 선언된 함수
nested function은 바깥에 선언된 함수의 변수들에 접근할 수 있다
또한 nested function자체가 return 될 수도 있다
그래서 다른 곳에서 쓰일때도 바깥에 있던 함수의 변수들을 쓸 수 있다

### Lexical Environment
자바스크립트에서 모든 함수, 코드 블록, 스크립트 전체는 Lexical Environment라고 하는 내부 객체?가 있다
두가지 부분으로 구성되는데
1. Environment Record - 모든 로컬 변수들이 저장되어있는 객체(+this의 value)
1. 바깥의 lexical environment를 참조하는 바깥 코드와 관련되어있는 부분
--------------------
변수는 단순히 특정 내부 객체의 속성이고, 변수를 바꾸는 것은 객체의 속성을 바꾸는 것
스크립트가 시작하면 Lexical Environment는 모든 선언된 변수들로 미리 채워진다 (상태는 uninitialized)
let이나 const로 선언되면 그때 value가 할당되고 이후에 변경하면 바뀐다
-----------------
함수 선언은 스크립트 시작과 함께 바로 준비된다
Lexical Environment가 만들어질 때 함수도 바로 사용가능한 상태임(let은 선언 코드를 만날때까지 사용할 수는 없다)
함수 표현식은 안됨
------------------
함수가 실행될 때, 지역변수들과 함수인자들을 저장하기 위해 Lexical Environment가 만들어진다
```javascript
let phrase = 'Hello';
function say(name) {
    alert(`${phrase}, ${name}!`);
};
say('John');
```
함수가 불리면 두개의 Lexical Environment가 생긴다. 안에 것과 바깥 것
inner Lexical Environment에 name: "John"
outer Lexical Environment에 phrase: "Hello", say: function
inner가 outer참조한다
변수는 inner부터 점점 out으로 찾아진다
-------------------
Function return할 때
```javascript
function makeCounter() {
  let count = 0;

  return function() {
    return count++; //<empty>
  };
}
let counter = makeCounter();
alert(counter()); //
```
모든 함수는 [[Environment]]라는 숨은 속성을 가지고 있고 함수가 만들어진 곳의 Lexical Environment를 계속 참조한다
counter.[[Environment]]는 {counter:0}Lexical Environment에 참조를 가지고있고 한번 저장되면 계속 유지되기 때문에 어디서 함수실행을 하든 변수를 계속 기억할 수 있다
counter가 call되면 먼저 익명 function으로 가서 Lexical Environment를 확인하는데 아무 변수가 없으니 <empty>상태가 되고, outer Lexical Environment를 참조하여 count를 찾게된다
counter가 여러번 call 되면 outer Lexical Environment의 count: 0이 count: 1로 변하게된다

```javascript
function count() {
    var i;
    for (i = 1; i < 10; i += 1) {
        setTimeout(function timer() {
            console.log(i);
        }, i*100);
    }
}
count();
// 10이 9번 출력된다
```
10이 9번 출력되는 이유는 0.1초 후에 timer()가 불리고 이 timer()는 i를 outer Lexical Environment에서 찾는다
그런데 0.1초 후에 i는 이미 10이 되어있어서 이후 9번 모두 10으로 출력이 된다
이것을 원래 의도대로 1부터 9까지 출력되게 하려면 for(let i=0; i<10; i+=1)로 바꿔주면 된다

##### 결론은 Javascript의 함수는 모두 클로져라고 할 수 있고 숨겨진 [[Environment]]라는 속성으로 어디에서 만들어졌는지 기억할 수 있어서 바깥변수들에 접근할 수 있다