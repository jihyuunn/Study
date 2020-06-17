# 표현식과 연산자

## 산술 연산자
1. 정수끼리 나눠도 부동소수점이 된다    
```javascript
7 / 2 // -> 3.5
```
2. 나머지 연산자 %의 피연산자는 부동소수점이다   
```javascript
5 % 1.5 // -> 0.5
```
3. + 에서 피연산자 중 하나가 문자열이면 나머지도 다 문자열로 만든다   
4. ++a(a에 1을 더하고 값을 평가), a++(a값을 평가하고 1을 더함)   
5. ** 제곱도 가능하다   

## Math객체의 프로퍼티
```javascript
Math.abs(x) // x의 절대값
Math.ceil(x) // x 이상 최초의 정수
Math.floor(x) // x 이하의 최대 정수
Math.max(a,b) //a,b중 큰값
Math.min(a,b) //a,b중 작은 값
Math.random() // 0이상 1미만의 난수
Math.round(x) // x반올림
Math.sqrt(x) //x의 제곱근
```

### 자바스크립트는 부동소수점으로 계산을 하기 때문에 정확도 문제가 생긴다 ( 0.16/0.2 => 0.799999 )

## 문자열 조작
- 문자열을 처리하기위한 객체로 원시값인 문자열을 String객체로 감싸는 것을 래핑이라고 한다   
```javascript
const strObj = new String('this is practice');
strObj.indexOf(s) //s가 처음 나오는 위치
strObj.lastIndexOf(s) //s가 마지막으로 나오는 위치
strObj.replace(s1,s2) // s1을 s2로 바꾸기
strObj.slice(m, n) // m이상 n미만 문자열 반환
strObj.startsWith(s, [,n]) // 대상 문자열의 n번째 문자부터 s로 시작하는지 판별한 논리값 리턴
```
- 문자열 단순 인덱싱도 가능하다. 그리고 문자열을 꼭 래핑할 필요없이 바로 메서드를 사용할 수 있는데 이것은 문자열에서 프로퍼티를 사용하려고 하면 내부적으로 String객체로 바뀌기 때문이다(-> 래퍼객체)   
- 보통 문자열은 래핑해서 사용하지 않고 그냥 래퍼객체를 사용한다. 왜냐면 원시값이 들어올 것으로 계획한 코드에 객체가 들어가면 오류가 생기기 때문   
 
## 논리 연산자와 관계 연산자   
### 1. 동일 연산자(==)와 일치 연산자(===)   
- ==는 내부적으로 두 변수의 타입을 변환시켜 똑같으면 true를 반환한다   
- ===는 타입이 다르면 false 리턴하고 타입까지 똑같아야 true를 반환한다   
```javascript
const a = 1;
const b = '1';
console.log( a == b ) // true 둘 중 하나가 숫자고 하나가 문자열이면 숫자로 바꿔서 비교
console.log( a === b ) // false
undefined == null;
true == 1; // 한쪽이 논리값이면 true를 1, false를 0으로 변환해서 비교
true == '1';
[2] == 2; // 한쪽이 객체면 객체를 toString이나 valueOf 메서드로 원시 타입으로 변환후 비교
```

### 2. 논리연산자 
- a&&b 에서 a를 평가한 값이 false면 어차피 false이기 때문에 b값을 평가하지 않고, false를 따로 리턴하는게 아니라 a값 자체를 리턴한다. a가 true면 b값을 리턴한다   
- a||b 에서 a를 평가한 값이 true이면 b에 관계없이 true가 되므로 a값을 리턴한다. a가 false이면 b의 값 자체를 리턴한다. 어떤 변수에서 초기값을 설정할 수 있지만 false로 인식되는 값0 등을 넘기면 초기값이 유지되는 단점이 있다.   

### 3. 기타 연산자
- typeof 원시 타입, undefined는 그대로 타입이 리턴되고, 함수이외의 객체(null포함)는 object로 리턴이 된다. 함수는 function 리턴   
- 조건 연산자
```javascript
const color = (a%2 == 0)? 'red' : 'blue';
```
- 쉼표 연산자
```javascript
let i = 0, sum = 0, product = 'eyewear';
for (let i =0, sum=0; i<10; i++) {
    sum += i
} // 이런 식으로 for문에 많이 쓰인다
```
- eval 함수 : python의 eval()과 같다   
- n.toString, String(n), parseInt() 등   

- 스프레드 연산자: 반복 가능한 객체의 모든 문자를 1개의 요소로 매핑   
```javascript
const name = [...'Lydia'];
console.log(name);
// ['L', 'y', 'd', 'i', 'a']
```