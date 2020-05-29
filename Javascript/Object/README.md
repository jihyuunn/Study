## Object   
- key, value값을 한쌍으로 만들어서 저장한 집합, key, value가 한 쌍을 이룬 것을 프로퍼티라고 하고, 그것의 이름을 프로퍼티 이름 또는 key라고 한다. value로는 모든 데이터 타입(원시값, 객체)를 저장 할 수 있고, 함수의 참조를 값으로 가진 프로퍼티를 메서드라고 한다.    

### 객체 생성   
```javascript
// 1 객체 리터럴
const card = { suit: "heart", rank: "A" };
// 2 생성자로 생성
function Card(suit, rank) {
    this.suit = suit;
    this.rank = rank;
}
const card = new Card('heart', 'A');
// 3 Object.create으로 생성
const card = Object.create(Object.prototype, {
    suit: {
        value: 'heart',
        writable: true,
        enumerable: true,
        configurable: true
    },
    rank: {
        value: 'A',
        writable: true,
        enumerable: true,
        configurable: true
    }
});
```

### prototype   
```javascript 
// 1
function Circle(center, radius) {
    this.center = center,
    this.radius = radius,
    this.area = function() {
        return Math.PI*this.radius*this.radius;
    }
}
// 2
function Circle(center, radius) {
    this.center = center,
    this.radius = radius
}
Circle.prototype.area = function() {
    return Math.PI*this.radius*this.radius;
}
```
- prototype프로퍼티는 기본적으로 빈 객체를 가리킨다   
- 1번 방식으로 area메서드를 생성자 안에 집어 넣으면 생성되는 모든 객체가 area메서드를 가지고 있기 때문에 메모리 낭비가 된다   
- 2번 방식으로 프로토타입 프로퍼티에 메서드를 지정하면 프로토타입 객체의 프로퍼티를 인스턴스에서 참조가능 -> '인스턴스가 프로토타입 객체를 상속하고 있다'   

