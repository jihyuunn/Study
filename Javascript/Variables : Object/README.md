# 변수

### var
- 호이스팅   
변수 선언은 가장 위로 끌어올려진다 그러나 대입부는 끌어올려지지 않는다   
```javascript
console.log(x) //undefined
var x = 5
```

### 변수타입
1. 원시값   
 문자열, 숫자, undefined(값을 할당하지 않았을 때, 함수에서 아무것도 리턴을 안할때, 없는 객체의 프로퍼티를 읽을 때, 없는 배열의 요소, 함수 호출 시 전달받지 못한 인수의 값), null, symbol, 논리값(true / false)     
- symbol : 자기 자신을 제외한 그 어떤 값과도 다른 유일무이한 값   

2. 객체값   
 여러 변수가 모여서 만들어진 복합 데이터 타입. 객체안에 값이 변할 수 있다. 배열, 함수, 정규 표현식      

# 1. 객체 리터럴
객체를 생성하는 방법은 1. 객체 리터럴로 생성하거나 2. 생성자를 사용할 수 있다   
```javascript
const card = {suit: 'spade', rank: 'A'};
const card = {'suit': 'spade', 'rank': 'A'}; //위랑 똑같다
card.suit //spade
card['rank'] //A
delete card.rank; //rank:'A'가 사라진다
console.log(color in card) //false를 리턴
```
- 생성된 객체는 메모리 영역을 차지하는 한 덩어리가 되고, 변수에 객체를 대입하면 변수는 객체의 참조가 저장된다(=변수는 객체를 참조한다)    
- 자바스크립트에서는 함수가 객체이다. 변수에 함수 객체의 참조가 저장되는 것.    
- 객체안에 함수가 있으면 메서드라고 한다   
- 함수로 넘겨야 하는 변수가 많으면 객체에 담아서 넘기면 된다. 단, 함수 안에서 객체가 변화하면 객체 프로퍼티 자체도 변한다(객체의 참조가 전달되기 때문)   
- 함수 선언문은 호이스팅이 되지만, 함수 리터럴은 호이스팅이 되지 않는다   
```javascript
// 함수 선언문
function square(x) {
    return x*x;
}
// 함수 리터럴
const square = function(x) {
    return x*x;
}
```

#### var / let / const
var: [선언 - 초기화 - 할당], let,const: [선언 - TDZ - 초기화 - 할당]   
- var는 함수 내부가 유효범위이고 let / const는 블록{} 이 유효범위이다.   
- var는 함수 내부에서 호이스팅이 되지만, let, const는 호이스팅이 안된다?
```javascript
var say = 'Hi';
{
    console.log(say); // Cannot access 'say' before initialization
    let say = 'Hello';
}
```
- 여기에서 호이스팅이 안되는 거라면 Hi가 출력이 됐어야하지만, 에러가 출력이 된다. 그렇기 때문에 호이스팅이 된다고 봐야한다. const도 마찬가지로 var는 선언과 초기화가 함께 되지만, let,const는 선언후에 TDZ(Temporal Dead Zone)에 의해 에러가 생김   
- let, const로 좀 더 엄격한 자바스크립트를 작성할 수 있고, 예기치않은 오류를 줄일 수 있다   

# 2. 객체 생성자
- 자바스크립트에 클래스는 없고 생성자라고하는 함수로 객체를 생성할 수 있다.   
```javascript
function Card(suit, rank) {
    this.suit = suit;
    this.rank = rank;
}
const card = new Card('heart', 'Q');
console.log(card); //Card {suit: 'heart', rank: 'Q'} 앞에 생성자 이름이 표시된다   
```
- 생성자 이름은 관례적으로 파스칼표기법(첫글자를 대문자로 쓰는 것)으로 한다   
- 생성자로 인스턴스(클래스로 생성한 실체)를 여러개 생성할 수 있다   

#### 내장 객체
- 사용자가 정의한 생성자 외에 자바스크립트에 처음부터 포함된 내장생성자가 있다   
- 내장 생성자에는 이미 유용한 프로퍼티와 메서드가 있으므로 다양한 작업을 쉽게 처리할 수 있다(Date, RegExp, Promise 등)   

#### 배열
- 배열을 변수에 대입하면 배열의 참조가 변수에 저장된다   
- []안에 담거나 new Array(Array;내장 생성자)로 만들 수 있다   
