# Class   
- 자바스크립트에서 클래스는 함수의 한 종류이다   
```javascript
class Person {
    constructor(name, age) {
        this.name = name,
        this.age = age
    }
    sayHi() {
        console.log('Hi'+this.name)
    }
}
```
1. 여기에서 Person이라는 이름을 가진 함수를 만들고 함수 본문은 생성자 메서드인 constructor안에서 가져온다    
2. sayHi와 같은 클래스 내에서 정의한 메서드는 Person.prototype 프로퍼티 안에 저장한다    

## 클래스 표현식   
```javascript
let Person = class {
    sayHi() {
        console.log("Hello World")
    }
}
```

## 클래스 상속   
```javascript
class Animal {
    constructor(name) {
        this.speed = 0;
        this.name = name;
    }
    run(speed) {
        this.speed = speed;
        console.log(`${this.name}이 ${this.speed}의 속도로 달립니다`)
    }
    stop() {
        this.speed = 0;
        console.log(`${this.name}이 멈췄습니다`)
    }
}
class Rabbit extends Animal {
    hide() {
        console.log(`${this.name}이 숨었습니다`)
    }
    stop() {
        super.stop(); //부모의 stop호출
        this.hide();
    }
}
let rabbit = new Rabbit('토끼');
```
- `rabbit.run(6)`을 호출하면 prototype체인으로 상속받은 클래스의 prototype을 참조한다   
- `super`는 부모 클래스에 정의된 메서드를 호출하거나 부모 생성자를 호출   
- `rabbit.stop()`은 부모 클래스에 정의된 stop()을 오버라이드 한다    