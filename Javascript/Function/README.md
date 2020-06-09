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

### 함수 리터럴과 화살표함수의 차이점   
1. 함수 리터럴은 함수를 호출할 때 this가 결정되지만, 화살표 함수의 this는 정의되면서 정해진다   
2. arguments 변수가 없다   
3. 생성자로 사용할 수 없다   
4. yield 키워드를 사용할 수 없다   

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

## apply / bind / call   
Function.prototype의 프로퍼티  
```javascript
const say = (greetings, honorifics) => {
    console.log(greetings + ' ' + honorifics + this.name)
};
const jihyun = { name: "Lee Jihyun" };
const harry = { name: "Harry Poter" };
say.apply(jihyun, ["Hello", "Ms"]);
say.apply(harry, ["Hi", "Mr"]);
say.call(jihyun, "hello", "Ms");
say.call(harry, "Hi", "Mr");
const sayToHarry = say.bind(harry);
sayToHarry("Hi","Mr");
``` 
- apply, call의 첫번째 인수는 함수의 this값이고 두번째 부터는 함수의 인수를 순서대로 담은 배열(apply) / 순서대로 넘기는 것(call)    
- bind는 함수의 this를 고정시킬 수 있다   
- apply, call은 함수가 실행이 되지만, bind는 실행이 되지않고 새로운 함수를 반환한다   
