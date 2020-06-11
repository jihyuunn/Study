### this   
1. 최상위 레벨 코드의 this   
-> 브라우저에서 window, Node에서는 global   
2. 이벤트 처리기 안의 this   
-> 그 이벤트가 발생한 엘리먼트   
3. 생성자 함수 안에 있는 this   
-> 생성자 함수로 생성한 객체   
4. 생성자의 prototype 메서드 안에 this   
-> 생성자로 생성한 객체   
5. 직접 호출한 함수 안에 있는 this   
-> 그 함수를 호출한 객체   
6. apply&call 메서드로 호출한 함수 안에 있는 this   
-> this가 가르키는 객체를 바꿀 수 있다   