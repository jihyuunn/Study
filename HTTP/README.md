## HTTP Hypertext Transfer Protocol
웹 브라우저와 웹 서버가 HTML로 작성된 웹 페이지나 동영상, 음성 파일 등을 주고받기 위한 통신규약   
stateless하게 이뤄진다 : 의미 이전 요청과 다음 요청이 서로 아무 관계가 없다
-> 이전에 로그인을 했던 정보가 다음 요청에 저장되지 않는다 (따로 처리를 해주어야 한다 sessionStorage)
![HTTP Message](./httpmessege.png)
- 시작줄에는 요청 혹은 요청의 성공실패가 기록되어있다   
- HTTP 헤더 세트가 들어가는데, 요청이나 바디에 대한 설명이 들어가있다   
- 빈줄   
- 바디   

## HTTP Methods
요청하는 데이터에 특정 동작을 수행하고 싶을 때
- GET, POST, PUT, DELETE
url과 http Methods는 클라이언트에서 설정해야하는 정보
http Status code와 응답 body 서버에서 보내주는 정보
- 2xx 성공
- 3xx 클라이언트가 이전 주소로 요청을 해서 새로운 url로 요청을 유도하는 경우
- 4xx 클라이언트 에러
- 5xx 서버 에러

## HTTPS HTTP Secure    
HTTP를 SSL로 암호화하여 보안성을 확보한 것   
HTTP의 문제점
1 자기가 요청하려 했던 서버에 리퀘스트를 보냈는지 확인할 수 없다
2 서버에서 응답을 보내는 클라이언트가 원래 의도한 리퀘스트를 보낸 클라이언트인지 확인할 수 없다
3 상대가 접근이 허가된 상대인지 확인이 불가하다
4 의미없는 리퀘스트도 받는다 -> Dos공격
-> SSL(Secure Socket Layer): 제 3의 기관에서 발행하는 증명서로 서버나 클라이언트가 실재함을 증명
HTTP는 원래 TCP와 바로 통신을 했지만 HTTPS는 SSL과 통신하고 SSL이 TCP와 통신   