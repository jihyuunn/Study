### Async Await
- function 앞에 async를 붙이면 언제나 promise를 반환한다
- async안에서 await을 만나면 async함수의 실행을 일시중지하고, await 뒤에 오는 프로미스의 해결을 기다린 다음 async 함수의 실행을 다시 시작하고 완료 후 값을 반환한다   
- await뒤에는 promise를 반환하는 함수를 실행시켜야한다 그냥 아무거나 실행한다고 await가 작동하지 않는다 그래서 axios, ajax같은 것들도 사실은 promise를 반환하는 메서드이다   
최상위 레벨에서는 사용할 수 없지만 익명함수로 감싸주면 사용할 수 있다   
```javascript
(async () => {
    let response = await axios.GET('some url');
})
```

### 에러 핸들링
성공적으로 이행되면 프라미스 객체의 result에 저장된 값을 반환하고, 실패하면 reject   
try...catch를 통해 await가 던진 에러를 잡을 수 있다   
async 함수 f()에 try...catch가 없으면 처리되지 않은 프라미스 에러가 발생한다   
f().catch(alert)의 형식으로 에러 처리를 해줘도 된다   
아니면 이전의 프라미스처럼 unhandledrejection 전역 이벤트 핸들러로 잡아줘도 됨   

대개 promise, then보다 async, await이 더 편하다   