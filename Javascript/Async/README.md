### Async Await
- function 앞에 async를 붙이면 언제나 promise를 반환한다
- async안에서 await을 만나면 프라미스가 처리될때까지 기다리고 처리되면 그 결과와 함께 다시 실행된다   
최상위 레벨에서는 사용할 수 없지만 익명함수로 감싸주면 사용할 수 있다   
```javascript
(async () => {
    let response = await axios.GET('some url');
})
```
- await는 Thenable객체를 받는다(promise가 아닌데 class안에 constructor와 then을 구현한 호출 가능한 객체)

### 에러 핸들링
성공적으로 이행되면 프라미스 객체의 result에 저장된 값을 반환하고, 실패하면 reject   
try...catch를 통해 await가 던진 에러를 잡을 수 있다   
async 함수 f()에 try...catch가 없으면 처리되지 않은 프라미스 에러가 발생한다   
f().catch(alert)의 형식으로 에러 처리를 해줘도 된다   
아니면 이전의 프라미스처럼 unhandledrejection 전역 이벤트 핸들러로 잡아줘도 됨   

대개 promise, then보다 async, await이 더 편하다