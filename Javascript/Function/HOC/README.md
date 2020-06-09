### 일급 객체   
아래의 세가지 조건을 만족하면 일급 객체라고 할 수 있다   
1. 변수나 데이터에 할당할 수 있어야한다   
2. 객체의 인자로 넘길 수 있어야한다   
3. 객체의 리턴값으로 리턴할 수 있어야한다   

### Higher Order Function   
아래 두가지 중 하나 이상을 만족하는 함수   
1. 함수를 파라미터로 넘겨받는 함수   
2. 함수를 리턴하는 함수   
이 조건을 만족시킬려면 기본적으로 일급 객체여야한다   
- React의 컴포넌트는 모두 HOC?   

### Currying   
커링이란 인수 두 개 이상을 받는 함수를 분해하여 인수가 하나인 함수의 중첩함수로 변환하는 작업   
가장 큰 장점은 부분 적용한 함수를 만들어낼 수 있다   
```javascript
const pow = function(exponent) {
    return function(base) {
        return Math.pow(base, exponent);
    }
};
const square = pow(2);
const sqrt = pow(.5);
```
