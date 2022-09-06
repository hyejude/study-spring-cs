*** GET, POST, PUT, DELETE

** REST
- 자원: URI
- 행위: HTTP Method
- 표현
즉, REST를 지키면서 행위를 전달하는 방법


** HTTP Method
- GET, POST, PUT, DELETE
보통 CRUD에서 조회-GET, 등록-POST, 수정-PUT, 삭제-DELETE


* 총 8개
GET  
POST  
PUT  
DELETE  
HEAD - 서버 리소스의 헤더 (메타 데이터 획득)  
OPTIONS - 리소스가 지원하고 있는 메소드 획득  
PATCH - 리소스 일부분 수정  
CONNECT - 프록시 동작의 터널 접속 변경  


* 멱등성(Idempotent)
여러 번 수행해도 결과가 같음, 호출로 인해 데이터가 변형되지 않음


* GET - 서버로부터 데이터 획득  
데이터 읽거나 검색할 때  
GET 요청이 성공적으로 실행되면 XML이나 JSON과 함께 200 HTTP 응답 CODE (OK) 리턴  
에러가 발생하면 주로 404 (Not Found) 에러나 400 (Bad Request) 에러 발생  
- 멱등성의 특징이 있음 - 같은 요청을 여러 번 해도 변함없이 항상 같은 응답 받음  
- 데이터를 읽을 때만 사용, 수정 될 때는 사용하지 않음 - 데이터 변경 연산에 사용하면 안됨  


`GET /user/1`  


- 데이터 조회 함수라 요청 시 BODY 값과 CONTENT-TYPE 비워져있음  
- 조회할 데이터 정보는 URL을 통해 PARA를 받고 있음  
- 데이터 조회에 성공하면 BODY 값에 데이터 저장하여 성공 응답 보냄  
- 캐싱 가능, 같은 데이터 한 번 더 조회할 경우 저장한 값 사용하여 조회 속도 증가  



* POST - 서버에 데이터 추가, 작성  
새로운 리소스 생성할 때 - 부모 리소스의 `하위 리소스` 생성 할 때  
성공적으로 CREATION 완료하면 201 (Created) HTTP 응답 반환  
- 멱등성 X - 같은 POST 요청 반복 실행해도 항상 같은 결과물 나온다는 보장 X  
- 두 개의 같은 POST 요청 보내면 같은 정보를 담은 두 개의 다른 리소스 반환 가능성 ↑  

`POST /user  
body : {date : 'example'}  
Content-type : 'application/json'`  

* PUT - 서버의 데이터 갱신, 작성  
리소스 생성/업데이트 하기 위해 서버로 데이터로 보내는 데 사용  
- 멱등성 - 동일한 PUT 요청 여러 번 호출 시 항상 동일한 결과  

`PUT /user/1  
body : {date : 'example'}  
Content-type : 'application/json'`  

- 데이터를 수정하는 거라 요청 시 BODY 값과 CONTENT-TYPE 작성해야 함 (해당 예시는 JSON 사용)  
- URL을 통해 어떤 데이터를 수정할지 PARA를 받음, 그리고 수정할 데이터 값을 BODY를 통해 받음  
- 데이터 조회 성공하면 BODY에 저장한 데이터를 저장해 성공 응답 보냄  

* DELETE - 서버의 데이터 삭제  
지정된 리소스 삭제  

`DELETE /user/1`  

- 데이터를 삭제하는 거라 요청 시 BODY 값과 CONTENT-TYPE 값 비워져있음  
- URL을 통해 어떤 데이터를 삭제할 지 PARA 받음  
- 데이터 삭제 성공하면 BODY 값 없이 성공 응답만 보냄  


* 참고 : velog.io/@yh20studio/CS-Http-Method-란-GET-POST-PUT-DELETE