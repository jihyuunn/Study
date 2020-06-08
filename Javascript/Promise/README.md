### Promise   
Promise 객체가 필요한 이유: 자바스크립트는 싱글스레드이기 때문에, 외부 API로 데이터를 받아오거나 web API(setTimeout, setInterval 등)을 처리할 때 코드 순서대로 처리가 되지 않는다. 그래서 비동기 처리를 위해 Promise가 필요하다    

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```
resolve(value) 함수가 제대로 처리되었을 때, reject(error) 에러가 발생했을 때 호출해야하고 둘 중 하나는 꼭 호출을 해야한다    
Promise 객체의 내부 프로퍼티 -> state, result     
- state: 처음엔 'pending'이었다가 resolve가 호출되면 'fulfilled', reject가 호출되면 'rejected'로 변한다   
- result: undefined였다가 resolve(value)가 호출되면 value, reject(error)가 호출되면 error로 변한다    

### promise 3가지 상태   
- pending: 이행되거나 거부되지 않은 초기의 상태   
- fulfilled: 연산이 성공적으로 완료됨   
- rejected: 연산이 실패함   
_new Promise -> state: "pending", result: undefined_    
_resolve(value) -> state: "fulfilled", result: value_    
_reject(error) -> state: "rejected", result: error_    
 
#### then
```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
promise.then(
    result => alert(result),
    error => alert(error)
);
```
then의 첫번째 인수는 promise가 이행되었을 때 실행되는 함수이고, 두번째 인수는 거부되었을 때 실행되는 함수이다  
성공적으로 이행된 경우만 다루고싶으면 인수를 하나만 넣으면 된다

#### catch
```javascript
promise.then(null, alert);
promise.catch(alert);
```
에러가 발생한 경우만 다루고 싶을 때는 then에 첫번째 인자로 null을 써주던지 catch를 통해 해주면 된다

#### finally
try / catch의 finally처럼 promise에도 finally가 있다
성공 실패 여부와 상관없이 실행된다

### Promise Chaining
연속적으로 비동기 처리를 하고싶을 때
```javascript
fetch('url')
    .then(response => response.json())
    .then(user => fetch(`url/${user}`))
    .then(response => response.json())
    .then(userImage => {
        //이미지 url을 가지고 body에 넣어주는 등의 처리를 해줄 수 있다
        //여기에 new Promise를 넣어주면 다음에 또 프라미스 체이닝이 가능하다 
        //new Promise가 resolve실행 완료시 다음 then이 실행된다
    })
```

### Promise Error Handling
프라미스 체인에서 에러가 발생하면 가장 가까운 rejection 핸들러로 넘어간다   
여러개의 then으로 체이닝을 하고 마지막에 catch로 에러 핸들러를 만들어주면 중간 어느곳에서 에러가 발생해도   
에러를 전부 잡을 수 있다   
=> 암시적인 try ... catch   
첫번째 catch블록에서 에러를 처리하고, 처리하지 못하면 또다시 throw Error를 통해 다음 catch블록으로 처리하지 못한 에러를 알려줄 수 있음   

#### Unhandledrejection
에러를 처리하지 못하면 스크립트가 죽고 콘솔창에 에러가 뜬다 -> 브라우저 환경에서는 이를 unhandledrejection을 통해 바로잡을 수 있다   
```javascript
window.addEventListener('unhandledrejction', function(event) {
  alert(event.promise);
  alert(event.reason);
})
```
HTML명세에 있는 표준 이벤트이고 .catch가 없으면 unhandledrejection이 실행된다   
이러한 처리 불가능한 오류는 사용자나 서버에 알려서 어플리케이션이 아무이유없이 죽는걸 방지해야 한다   

#### Microtask Queue
```javascript
let promise = Promise.resolve();
promise.then(() => alert('promise success'));
alert('promise ended');
```
위의 코드에서 프라미스 종료가 프라미스 성공보다 먼저 뜨는 이유는 현재 코드가 모두 실행되고 나서 큐가 실행되기 때문이다   
.then/catch/finally는 microtask queue에 들어간다고 생각하면 된다   
unhandledrejection은 마이크로태스크 큐 끝에서 에러가 처리되지 않으면 실행된다   

```javascript
let promise = Promise.reject(new Error("프라미스 실패!"));
setTimeout(() => promise.catch(err => alert('잡았다!')), 1000);

// Error: 프라미스 실패!
window.addEventListener('unhandledrejection', event => alert(event.reason));
```
여기에서 "프라미스 실패"가 먼저 출력되고 그 다음 "잡았다"가 출력되는데 프라미스를 검사하고 하나라도 rejected상태이면 unhandledrejection이 트리거 된다   
.catch로 에러가 잡히기는 하지만, unhandledrejection이 트리거 된 이후에 트리거 되므로 unhandledrejection이 작동된다   
