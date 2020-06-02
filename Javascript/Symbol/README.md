## Symbol   
- Symbol은 프로그램 전체에서 유일한 값이다. 원시형 값이다.   
- 선언 될 때마다 새로운 값이라고 보면 된다   
```javascript
const first = Symbol('A');
const second = Symbol('A');
first === second; // false
```
### Symbol의 도입 이유    
- 프로퍼티 이름의 충돌을 막기 위해서 -> 심볼은 객체에 직접 접근을 못하기 때문에(외부에서 접근 불가능)   
```javascript
// 서드파티에서 가져온 객체
const userInformation = {
    name: 'john',
    age: 14,
}
// 첫번째 라이브러리에서 식별자를 부여하고 싶을 때
let id = Symbol('id');
userInformation[id] = 123;
console.log(userInformation) // {name:'john', age: 14, Symbol('id'): 123}
// 두번째 라이브러리에서 식별자를 부여하고 싶을 때
let id = Symbol('id');
userInformation[id] = 234;
console.log(userInformation) // {name:'john', age: 14, Symbol('id'): 123, Symbol('id'): 234}
```

### 특징    
1. Symbol은 값을 외부에 노출시키지 않는다   
2. 객체의 키값으로 지정 가능(원래는 string만 가능했다)   
3. Symbol은 getOwnPropertyNames 반환값에서 나오지 않고, for loop에서도 나오지 않는다   
 -> getOwnPropertySymbols 사용   
