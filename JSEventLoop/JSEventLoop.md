## Event Loop
Event Loop이라는 말 그대로 무한으로 계속 Call Stack을 확인하며 실행해야하는 작업이 있는지 확인 하는 것
Call Stack / Callback Queue / Web API
```javascript
console.log('Hi'); //1
setTimeout(function cb1() { 
    console.log('cb1'); //4
}, 5000); //2
console.log('Bye'); //3
```
1이 Call Stack에 들어갔다가 출력이 되면 pop된다
2가 Call Stack에 들어가면 Web API에서 5초를 잰다 실행 후 pop된다
3이 Call Stack에 들어갔다가 출력 후 pop
Web API에서 5초가 지난 후에 콜백cb1()을 Callback Queue에 넣는다
Event Loop이 Call Stack에 아무것도 없기 때문에 Callback Queue에 있던 cb1()을 Call Stack에 넣는다
4가 Call Stack에 들어간다
cb1출력 후 4 pop, cb1() pop

- setTimeout의 의미는 n초 후에 실행이 아니라 n초 후에 Queue에 들어간다는 의미
