## Prototype    
자바스크립트 객체는 [[Prototype]]이라는 숨김 프로퍼티를 갖는다   
프로퍼티를 읽으려고 할 때 없으면 자동으로 프로토타입에서 프로퍼티를 찾는다   
프로토타입 체이닝이 가능하다 하지만 순환참조는 안되며, __proto__의 값은 객체나 null만 가능하다    

### Prototype 상속   
```javascript
let animals = {
    eats: true
};
function Rabbit(name) {
    this.name = name
};
Rabbit.prototype = animals;
let rabbit = new Rabbit("white rabbit");
console.log(rabbit.eats); // true
```
- 여기에서 Rabbit.prototype의 prototype은 Rabbit에 정의된 일반 프로퍼티이다. new Rabbit을 호출해서 만든 새로운 객체의 [[Prototype]]이 animals로 설정이 된다.    
- 일반 객체에 prototype 프로퍼티를 만들면 아무일도 일어나지 않는다    
```javascript
const A = [1,2,3];
const B = () => {};
const C = 'string';
const D = true;
```
- 이 때 각각 A, B, C, D는 Array.prototype, Function.prototype, String.prototype, Boolean.prototype을 상속받고 이 네가지는 모두 Object.prototype을 상속받는다   
