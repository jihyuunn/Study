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