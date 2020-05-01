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

### Break/Continue   
- 라벨을 지정한 break문을 실행하면 라벨이 붙은 문장 끝으로 점프한다   
```javascript
const a = [1,2,3,4,5], b = [3,4,5,6,7];
loop: for (let i=0;i<a.length;i++) {
    for (let j=0;j<b.length;j++) {
        if (a[i]===b[j]) break loop
    }
}
console.log(`a[${i}], b[${j}]`)
// a[2], b[0]
```
- continue에도 라벨을 지정하면 라벨이 붙은 문장의 처음으로 돌아가서 다시 조건 검사를 한다   
