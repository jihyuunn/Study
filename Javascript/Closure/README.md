### nested function
함수 안에 선언된 함수
nested function은 바깥에 선언된 함수의 변수들에 접근할 수 있다
또한 nested function자체가 return 될 수도 있다
그래서 다른 곳에서 쓰일때도 바깥에 있던 함수의 변수들을 쓸 수 있다

## Closure
#### 함수 객체 + 렉시컬 환경 컴포넌트    
- scope chain과 헷갈리는 부분이 많았다. 하지만 스코프 체인은 그냥 단순히 outer lexical environment를 거슬러 올라가서 필요한 변수를 참조하는 것이라면, 클로저는 이미 execution stack에서 바깥쪽의 함수가 빠져나갔음에도 그 함수안에 선언된 변수를 기억하고 사용하는 것이다   
```javascript
function count() {
    var i;
    for (i = 1; i < 10; i += 1) {
        setTimeout(function timer() {
            console.log(i);
        }, i*100);
    }
}
count();
// 10이 9번 출력된다
```
- 위의 코드가 클로저 예시인 이유는 count()가 call stack에서 빠져나가고난 후에 setTimeout의 콜백 함수인 timer()가 call stack으로 들어가기 때문이다. timer()의 클로저가 outer lexical environment를 기억하고 있기 때문에 i를 사용할 수 있다.    
1. 0.1초 후에 i는 전역객체이기 때문에(함수 내에서) 이미 10이 되어있어서 이후 9번 모두 10으로 출력이 된다    
2. for(let i=0; i<10; i+=1)로 바꿔주면, let의 유효범위가 block scope이기 때문에 timer()가 콜스택으로 들어갈 때마다 execution context가 생기고 그 당시의 i값을 기억하기 때문에 1부터9까지 출력이 된다   

### Garbage Collection
보통 함수 call이 끝나면 Lexical Environment는 메모리에서 삭제된다(더이상 참조하지 않아도 되기때문)
그런데 함수가 끝난 후에도 nested function이 계속 접근가능하면 Lexical Environment를 참조하는 [[Environment]]가 계속 있게된다
