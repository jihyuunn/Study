# 제어구문

- 조건문: if/else, switch, try/catch/finally   
- 반복문: while, do/while, for, for/in, for/of   
- 점프문: break, continue, return, throw   

### Switch   
분기점을 여러개 만들 때 if/else문보다 더 간결하게 표현가능하다   
```javascript
switch(n) {
    case 1: // === 일치연산자로 확인하는 방법과 같다
        console.log('one');
        break;
    case 2: 
        console.log('two');
        break;
    case n: 
        console.log('n');
        break;
    default: 
        console.log('number');
}
```
- break를 쓰지 않으면 case라벨로 분기한 다음에 그 라벨 뒤에 등장하는 전체 문장을 실행한다 break를 만나야 switch문을 빠져나온다   

### Do/While   

### For/In
```javascript
const obj = {a:1, b:2, c:3};
for (let i in obj) {
    console.log(obj[i])
}
// 1, 2, 3 순서대로 출력
```
