# REST   
- Representational State Transfer   
- HTTP URI를 통해 자원을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD처리를 하도록 하는 것   
- resource들을 하나의 엔드포인트에 연결해놓고, 각 엔드포인트는 그 resource와 관련된 내용만 관리   

1. URI는 정보의 자원을 표현해야한다   
2. 자원에 대한 행위는 HTTP method로 들어가고, URI에 들어가면 안된다   
3. (-)사용가능 (_)사용하지 않음   
4. 소문자 사용   
5. 파일 확장자를 URI에 포함시키지 않는다   

|HTTP method|Route|CRUD|
|:---:|:---:|:---:|
|`GET`|/users|모든 유저의 정보|
|`GET`|/users/:id|특정 유저의 정보|
|`POST`|/users|새로운 유저 생성|
|`PUT`|/users/:id|특정 유저의 정보 수정|
|`PATCH`|/users/:id|특정 유저의 정보 수정|
|`DELETE`|/users/:id|특정 유저의 정보 삭제|

*PUT은 모든 필드의 정보를 다 전달해줘야하고, PATCH는 전달된 필드의 정보만 수정한다*