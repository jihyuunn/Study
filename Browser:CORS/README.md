### Browser
브라우저의 주요 기능은 사용자가 선택한 자원을 서버에 요청하고 브라우저에 표시해주는 것   
HTML과 CSS의 명세에 따라 해석해서 보여주고 이 명세는 W3C 표준을 따른다   

1. 사용자인터페이스   
2. 브라우저 엔진 : 사용자 인터페이스와 렌더링 엔진 사이를 제어   
3. 렌더링 엔진 : HTML과 CSS를 파싱하여 보여주는 것 처럼 요청한 콘텐츠를 보여준다
4. 통신 : HTTP와 같은 네트워크 호출에 사용됨   
5. UI backend : 인풋박스?와 같은 플랫폼에서 명시하지 않은 장치에 대해 사용자 OS 인터페이스에 따라 보여줌   
6. 자바스크립트 해석기 : 자스코드를 해석하고 실행   
7. 자료저장소 : 쿠키 등 저장

### 브라우저 동작 원리
1. HTML 파싱하여 DOM 트리를 빌드한다   
2. 파싱하는 도중 CSS 파일 링크를 만나면 요청하여 받아온다   
3. CSS를 처리하여 CSSOM 트리를 만든다   
4. DOM과 CSSOM을 합쳐서 렌더링 트리를 만들고 노드는 CSS박스모델을 만든다(어디에 위치할지 계산하는 것)   
5. 개별 노드를 화면에 페인트한다   

### CORS Cross Origin Resource Sharing  
<img>, <link>와 같은 태그 안에서는 다른 도메인의 정보를 불러올 수 있지만 <script>안에서는 다른 도메인의 정보 요청이 안된다   
Same Origin Policy : 대부분의 브라우저들이 보안상의 이유로 스크립트에서 Cross-Origin HTTP요청을 제한한다 -> 요청을 보내려면 요청을 보내는 서버와 프로토콜, 포트번호까지 똑같아야된다   
그래서 CORS가 타 도메인 간에 자원공유를 가능하게 해준다   
+ 'domain1.com' -> 'domain2.com' url이 아예 다르면 요청안됨   
+ 'domain.com:3000' -> 'domain.com:8000' 포트번호가 달라도 요청이 안된다    

### CORS 해결방법    
- 가장 좋은 방법은 서버쪽에서 해당 도메인에 대한 요청을 허용하는 것이다 (Access-Control-Allow-Origin에서 도메인을 허용해주거나, node에서는 CORS미들웨어를 설치할 수 있다) 
- create-react-app에서 package.json에 proxy로 root도메인을 등록해주면 되는데 build하고서는 안된다고 한다.. 또는 jsonp를 사용가능 


### Simple Request
어떤 요청들은 preflight를 만들어내지 않는데 이것을 simple request라고 한다   
- GET, HEAD, POST 중 한가지 메서드만 가능하다
- 커스텀 헤더를 전송하면 안된다(Accept, Content-Language, Content-Type 등 몇개만 가능)
- Content-Type 헤더에서 *application/x-www-form-urlencoded, multipart/form-data, text/plain* 이 세개만 value로 들어갈 수 있다   
```
GET /resources/public-data/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
...
Origin: https://foo.example

HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2
Access-Control-Allow-Origin: *
...
Content-Type: application/xml
```
request에서 _Origin_ 을 보면 이 요청이 어디서부터 오는건지 알려주고, response를 보면 _Access-Control-Allow-Origin_ 여기에서 어떤 도메인이든 접근가능하다는 것을 알려준다

#### Preflight
Simple Request의 조건에 맞지 않으면 preflight 방식으로 요청   
실제로 요청하려는 경로와 같은 URL에 대해 OPTIONS 메서드로 요청을 먼저 날려보고 요청할 권한이 있는지 확인한다   
클라이언트의 처리만으로는 안되고 해당 서버 측에서 추가 처리 사항이 필요하다   
서버에서 : _Access-Control-Allow-Origin: *_, _Access-Control-Allow-Methods: GET,POST,PUT_ 등의 처리   
-> 모든 요청의 응답 header에 위 항목을 포함시킨다   
```
OPTIONS /resources/post-here/ HTTP/1.1
...
Origin: http://foo.example
Access-Control-Request-Method: POST 
Access-Control-Request-Headers: X-PINGOTHER, Content-Type

HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER, Content-Type
Access-Control-Max-Age: 86400
```
- 첫번째 줄에서 *OPTIONS* 라는 메서드로 프리플라이트 리퀘스트를 보내고있다   
- Access-Control-Request-Method 실제 요청이 전달될 때 어떤 메서드로 갈지 알려줌   
- Access-Control-Request-Headers 실제 요청이 갈 때 'X-PINGOTHER, Content-Type' 두개의 커스텀 헤더가 같이 갈 것임을 알려줌 -> 서버가 이런 조건에서 이제 리퀘스트를 받아들일지 결정할 수 있다   
- Access-Control-Allow-Headers 두 개의 커스텀 헤더가 허락되는 것을 컨펌해줌   
- Access-Control-Max-Age 이제 또 다른 프리플라이트 없이 요청이 가능한지 = 현재 프리플라이트가 캐시 저장되는 초(86400=하루)   


프리플라이트 리퀘스트가 완료되면 진짜 리퀘스트가 보내짐
```
POST /resources/post-here/ HTTP/1.1
...
X-PINGOTHER: pingpong
Content-Type: text/xml; charset=UTF-8
Referer: https://foo.example/examples/preflightInvocation.html
Content-Length: 55
Origin: https://foo.example
Pragma: no-cache
Cache-Control: no-cache

HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://foo.example
...
Content-Type: text/plain
```