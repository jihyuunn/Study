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
        EnvironmentRecord: {
            // 선언적 환경 레코드   
            DeclarativeEnvironmentRecord: {},   
            // 객체환경 레코드   
            ObjectEnvironmentRecord: {}   
        },   
        // 외부 렉시컬 환경 참조
        OuterLexicalEnvironment Reference: {}
    },
    // 변수 환경 컴포넌트
    VariableEnvironment: {
        // Lexical Environment와 내부 값이 똑같다
    },
    // 디스 바인딩 컴포넌트
    ThisBinding: null
}
```
- 렉시컬환경 컴포넌트와 변수 환경 컴포넌트는 타입이 같고 실제로 거의 내부 값이 같아서 똑같이 취급해도 무리가 없다   
- 디스 바인딩 컴포넌트는 그 함수를 호출한 객체의 참조가 저장되는 곳 = 해당 실행 문맥의 this가 된다   

### Lexical Environment   
자바스크립트 엔진이 자바스크립트 코드를 실행하기 위해 자원을 모아둔 곳   
-> 함수 또는 블록의 유효범위 안에 있는 식별자와 그 결과값이 저장된다(key, value로 저장됨)   
EnvironmentRecord와 OuterLexicalEnvironment Reference로 구성됨   
- EnvironmentRecord: 유효범위 안에 식별자를 기록, 실행   
- OuterLexicalEnvironment Referene: 함수를 둘러싸고 있는 코드가 속한 렉시컬 환경 컴포넌트의 참조가 저장된다. 중첩된 함수 안에서 바깥 코드에 정의된 변수를 읽거나 써야할 때 OuterLexicalEnvironment Referene를 따라 한단계씩 거슬러 올라가서 그 변수를 검색한다   

#### 1. Environment Record      
렉시컬 환경 컴포넌트의 구성요소, 렉시컬 환경 안의 식별자와 그 값이 실제로 저장되는 영역.   
선언적 환경 레코드와 객체 환경 레코드로 구성되어있다   
1-1. DeclarativeEnvironment Record(선언적 환경 레코드): 실제 함수와 변수, catch문의 식별자와 실행결과가 저장되는 영역   
1-2. ObjectEnvironment Record(객체 환경 레코드): 실행 문맥 외부에 별도로 저장된 객체의 참조에서 데이터를 읽거나 씀. 전역객체같은 데이터를 복사해오는게 아니라 참조를 가져와서 객체환경레코드의 bindObject라는 프로퍼티에 바인드하게 되어있다     
```
ExecutionContext: {
    LexicalEnvironment: {
        ObjectEnvironmentRecord: {
            bindObject: window
        },
        // 전역환경 바깥의 환경은 없다
        OuterLexicalEnvironmentReference: null 
    },
    ThisBinding: window
}
```
```javascript
var a = {x:1, y:2};
console.log(window.a) // Object {x:1, y:2}
function norm(x) {...}
console.log(window.norm) // norm(x)
```
- 전역 변수는 전역 객체의 실행문맥(ExecutionContext)에 들어있는 객체환경레코드(ObjectEnvironmentRecord)의 프로퍼티이다 == 객체환경레코드에 바인드 되어있는 window의 프로퍼티가 된다   
- 최상위에서 선언된 변수와 함수는 프로그램 평가하는 시점에 객체환경레코드에 추가가된다. 그래서 어느 위치에 작성을 해도 프로그램이 참조할 수 있는데 이것이 *호이스팅* 이다   

### 자바스크립트 싱글스레드   
- 실행되는 함수는 호출 스택에 쌓이기 때문에 LIFO로 실행이 된다. 하나의 실행이 끝날때까지 다른 함수가 실행이 되지 않는다   
- 이벤트 처리와 같은 비동기 처리도 똑같은 방식으로 실행한다. 실행 준비를 마친 이벤트처리기 함수와 비동기 처리는 실행하기에 앞서 이벤트 큐에 들어간다. 그리고 현재 실행중인 함수의 작업이 끝나면 이벤트 큐의 첫번째부터 차례대로 호출 스택에 push해서 실행한다   

### 환경 레코드와 지역변수   
- 함수를 호출하면 현재 실행중인 코드의 작업을 일시적으로 멈추고 실행문맥(Execution Context)을 생성 -> 함수의 실행 문맥이 호출스택에 push되고 실행 문맥 안에 렉시컬 환경 컴포넌트 생성 -> 렉시컬 환경 컴포넌트 안에 환경 레코드(함수 안에 선언된 변수들이나 전역 객체 등)와 외부 렉시컬환경 참조가 기록된다 -> ThisBinding컴포넌트에 그 함수를 호출한 객체의 참조를 저장하고 이것으로 this값을 결정 -> 함수안의 코드가 순서대로 실행( 이 시점에 이미 함수안에 있는 변수나 함수가 이미 선언적 환경 레코드에 저장되어있는 상태이기 때문에 함수안의 어디에 위치하더라도 접근할 수 있다=호이스팅이 되는 이유 ) -> 함수가 종료되어 제어권이 호출한 코드로 돌아가면 실행문맥과 그 안의 렉시컬환경컴포넌트가 메모리에서 지워진다    

### this   
1. 최상위 레벨 코드의 this   
2. 이벤트 처리기 안의 this   
3. 생성자 함수 안에 있는 this   
4. 생성자의 prototype 메서드 안에 this   
5. 직접 호출한 함수 안에 있는 this   
6. apply&call 메서드로 호출한 함수 안에 있는 this   

### 스코프 체인   
```javascript
var a = 'A';
function f() {
    var b = 'B';
    function g() {
        var c = 'C';
        console.log(a+b+c)
    }
}
```
```
g_LexicalEnvironment: {
    EnvironmentRecord: {
        DeclarativeEnvironmentRecord: {
            c: 'C'
        }
        ObjectEnvironmentRecord: { }
    },
    OuterLexicalEnvironment: {
        f_LexicalEnvironment
    }
}
f_LexicalEnVironment: {
    EnvironmentRecord: {
        DeclarativeEnvironmentRecord: {
            b: 'B'
        }
        ObjectEnvironmentRecore: { }
    }, 
    OuterLexicalEnvironment: {
        global_LexicalEnvironment
    }
}
global_LexicalEnvironment: {
    EnvironmentRecord: {
        DeclarativeEnvironmentRecord: {},
        ObjectEnvironmentRecord: {
            bindObject: {
                a: 'A'
            }
        }
    },
    OuterLexicalEnvironment: null
}
```

### Closure   
Closure = 함수 객체 + 렉시컬 환경 컴포넌트   
함수 객체가 참조하는 렉시컬 환경은 가비지 컬렉션의 대상이 되지않는다   

### 함수 리터럴과 화살표함수의 차이점   
1. 함수 리터럴은 함수를 호출할 때 this가 결정되지만, 화살표 함수의 this는 정의되면서 정해진다(window)   
2. arguments 변수가 없다   
3. 생성자로 사용할 수 없다   
4. yield 키워드를 사용할 수 없다   
