### XMLHttpRequest
XMLHttpRequest는 자바스크립트에서 HTTP 요청을 보낼 수 있게 해주는 브라우저에서 제공하는 것이다
XML말고 다른 여러가지도 보내거나 받을 수 있다
fetch가 더 최신의 방법이다
최신 개발에서 XMLHttpRequest를 사용하는 이유는 3가지이다
1. 예전에 쓰던것이어서 계속 사용해야할 때
1. 폴리필을 하고싶지 않을 때, 오래된 브라우저를 지원하기 위해서
1. fetch가 아직 못하는 것을 해야할 때(업로드 과정을 추적)

```javascript
let xhr = new XMLHttpRequest();
xhr.open('POST', 'https://www.google.com', false, user, password);
// method, url, [async, user, pwd](http 권한을 위한 것 필요할 때만 써주면 됨)
xhr.responseType = 'json';
xhr.send([body])
```
- xhr.open이 connection을 오픈하는 것은 아니고 send에서 연결이 되고 서버로 리퀘스트를 보낸다
- GET같은 경우 body가 필요없고 POST같이 필요한 경우만 채움
- async 여부 자리에 false를 써주면 동기처리가 되고 xhr.send를 try/catch안에 넣어서 처리가능   그러나 동기처리 안하는게 낫다 페이지 안의 자스까지 멈춰버릴 수 있기 때문

```javascript
xhr.onload = function() {
  if (xhr.status != 200) { 
    alert(`Error ${xhr.status}: ${xhr.statusText}`); // e.g. 404: Not Found
  } else { 
    alert(`Done, got ${xhr.response.length} bytes`); // responseText is the server
  }
};

xhr.onprogress = function(event) {
  if (event.lengthComputable) {
    alert(`Received ${event.loaded} of ${event.total} bytes`);
  } else {
    alert(`Received ${event.loaded} bytes`); // no Content-Length
  }

};

xhr.onerror = function() {
  alert("Request failed");
};
```
- onload는 HTTP status(400, 500이어도)에 상관없이 리퀘스트가 끝나고 응답이 오면 실행된다
- onprogress는 주기적으로 실행된다. event.loaded: 몇 바이트가 다운로드 되었는지, event.total: 전체 바이트
- onerror 리퀘스트가 아예 안될 경우 

```javascript
let xhr = new XMLHttpRequest();

let json = JSON.stringify({
  name: "John",
  surname: "Smith"
});

xhr.open("POST", '/submit')
xhr.setRequestHeader('Content-type', 'application/json; charset=utf-8');

xhr.send(json);
```
- POST요청 보낼 때 json으로 보낼 수 있다. 그때는 header 설정을 저렇게 해줘야 서버에서 인식 가능하다