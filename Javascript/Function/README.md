# 함수   

## 함수를 정의하는 방법   
1. 함수 선언문
```javascript
function sayHi() {
    console.log('Hi')
}
```
2. 함수 리터럴   
```javascript
const sayHi = function() {
    console.log('Hi')
}
```
3. Function 생성자
```javascript
const sayHi = new Function( ,console.log('Hi'));
```
4. 화살표 함수 표현식
```javascript
const sayHi = () => console.log('Hi');
```
##### 여기에서 호이스팅이 되는 것은 함수 선언문 밖에 없다(호이스팅이 되지만, const로 선언을 했기 때문에 TDZ 상태이기 때문에 에러가 난다고 하는 것이 맞을 것 같다)   
- 자바스크립트에서는 최상위 함수에 중첩함수를 사용할 수 있다   

## 함수를 호출하는 방법   
- 함수 호출, 메서드 호출, 생성자 호출, call/apply를 사용한 간접 호출

## 함수의 인수   
- 함수를 호출할 때 인수를 생략   
인수에서 생략한 인자는 undefined가 된다. 인수를 생략했을 때 쓸 초깃값을 설정하면 된다.   
```javascript
const multiply = (a,b) => {
    b = b||1;
    return a*b
};
multiply(2);
// 2
```
- 함수를 호출할 때 더 많은 인수를 넘기기   
모든 함수에서 사용할 수 있는 지역변수로는 arguments변수가 있다. arguments 변수의 값은 Arguments객체이다. 함수에 인수 n개를 넘겨서 호출하면 인수값이 arguments에 저장된다. Arguments 객체의 프로퍼티는 arguments.length:인수의 개수, arguments.callee:현재 실행되고 있는 함수의 참조      
```javascript
const addString = separator => {
    let s = '';
    for (let i=1; i<arguments.length; i++) {
        s += arguments[i]
        if (i<arguments.length-1) {
            s += separator
        }
    }
}
addString('/', 'apple', 'orange', 'banana');
// apple/orange/banana
```
- 첫번째 인자는 separator와 arguments[0]에 할당이 된다. 그리고 나머지 인자들은 argument[1]부터 순서대로 할당이 된다.   

## 재귀함수   
재귀함수는 재귀 호출로 문제를 간단하게 풀 수 있을 때 사용한다. 함수를 새로 호출할 때마다 메모리의 다른 영역을 사용하기 때문에 while/for문으로 작성하는 것이 이해하기 쉽고 메모리 공간을 적게 차지한다   

## 프로그램 평가와 실행과정   
- 실행 가능한 코드: 전역코드, 함수코드, eval코드   
- 실행문맥 Execution Context: 실행 가능한 코드가 실제로 실행되고 관리되는 영역
```javascript
ExecutionContext = {
    // 렉시컬 환경 컴포넌트
    LexicalEnvironment: {
        // 환경 레코드
        EnvironmentRecord: {},
        // 외부 렉시컬 환경 참조
        OuterLexicalEnvironment Reference: {}
    },
    // 변수 환경 컴포넌트
    VariableEnvironment: {},
    // 디스 바인딩 컴포넌트
    ThisBinding: null
}
```
- 렉시컬환경 컴포넌트와 변수 환경 컴포넌트는 타입이 같고 실제로 거의 내부 값이 같아서 똑같이 취급해도 무리가 없다   
- 디스 바인딩 컴포넌트는 그 함수를 호출한 객체의 참조가 저장되는 곳 = 해당 실행 문맥의 this가 된다   