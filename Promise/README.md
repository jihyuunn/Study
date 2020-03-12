### Promise

```javascript
let promise = new Promise(function(resolve, reject) {
  // executor (the producing code, "singer")
});
```
resolve(value) 함수가 제대로 처리되었을 때    
reject(error) 에러가 발생했을 때    
new Promise constructor에 리턴된 promise 객체는 state, result 속성을 가지고 있다    
_new Promise -> state: "pending", result: undefined_    
_resolve(value) -> state: "fulfilled", result: value_    
_reject(error) -> state: "rejected", result: error_    
오직 한번의 resolve / reject가 실행된다
 
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

