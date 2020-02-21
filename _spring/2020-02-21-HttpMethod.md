## HTTP Method 종류와 역할
**(1) GET**
   - URI(URL)가 가진 정보를 검색하기 위해 서버 측에 요청하는 형태이다.
   - 웹서버측 리소스(데이터)를 요청

**(2) HEAD**
   - 메세지 헤더(문서 정보) 취득
   - GET과 비슷하나, 실제 문서를 요청하는 것이 아니라, 문서 정보를 요청
   - 이에따라 HTTP 응답 메세지에 본문(Body)이 없이 HTTP 헤더 정보 만을 보낸다.

**(3) POST**
   - 내용 전송 (파일 전송 가능)
   - 클라이언트에서 서버로 어떤 정보를 제출함
   - 요청 데이터를 HTTP 바디에 담아 웹서버로 전송함
   - 만일, 리소스가 새로이 작성되면, 서버측은 HTTP 헤더 항목 중 `Location:`에다가 새로이 작성된 리소스에 대한 URI 주소 정보를 포함시켜 응답하게 된다.


**(4) PUT**
   - 내용 갱신 위주 (파일 전송 가능)
   - POST 처럼 정보를 서버로 제출하는 것으로 형식은 동일하나, 갱신 위주 이다.
   - 이에 의해 갱신된 리소스에 대한 주소 정보를, POST와는 달리
   - 서버측 응답메세지의 HTTP 헤더 항목 중에 `Location:`을 보내지 않아도 된다.
   - 즉, 서버측은 클라이언트 측이 제시한 URI를 그대로 사용하는 것으로 간주한다
   - PUT는 클라이언트측이 서버측 구현에 관여하는 것이므로, 
   - 통상 보다 세밀한 POST를 더 많이 쓴다

**(5) DELETE**
   - 파일 삭제 
   - 웹 리소스를 제거

**(6) OPTIONS**
   - 웹 서버측 제공 메소드에 대한 질의
   - 가능한 메소드 옵션에 대한 질의
   - 이 경우 응답메세지에 HTTP 헤더 항목 중 ‘Allow : GET,POST,HEAD’처럼 보내게 됨

**(7) TRACE** (거의 사용하지 않는다)
   - 요청 리소스가 수신되는 경로를 보여준다.

**(8) CONNECT** (거의 사용하지 않는다)
   - 프락시 서버와 같은 중간 서버 경유
   - 例) 웹브라우저는 `CONNECT www.original_server.com:80 HTTP/1.0` 뒤에,
   - 일련의 HTTP 헤더 항목들과 빈 줄(CRLF)로써 프록시 서버에게,
   - 원하는 웹서버와의 중계 연결 요청을 한다



  ※ 한편, 보안상의 이유로, 웹서버가 GET,POST 2개 또는 OPTIONS 포함 3개 만을 허용하는 경우가 대부분이다.
  
  -------------------------------------------------------------------------------------------------
  
  ##### 1. 응답코드는 상태 코드와 응답 구문으로 이루어져있습니다. 
```
1xx Informational (요청받은 처리가 계속되고 있을 때)

2xx Success(요청이 성공했을 경우)

3xx Redirection (클라이언트가 요청한 컨텐츠가 다른 곳에 있다는 의미)

4xx Client Error(클라이언트로 인한 오류로 요청 실패)

5xx Server Error(서버측의 오류로 요청 실패)
```
   
   ---------------------------------------------------------------------------------------------------
   
#### 1. POST 로 요청한 경우 성공시 응답코드는 무엇으로 올까?
```
  200번이라고 생각한 이유는 대부분의 성공 코드가 200번이기 때문입니다.
하지만 질문은 post로 요청시 응답코드라는 것을 생각했을 때 201번으로 와야할거같습니다!!
201번은 새로운 컨텐츠 만들기에 성공했을 때 사용하기 때문입니다. 
클라이언트에서 서버로 새로운 글이나 댓글 정보를 담아 제출하면 서버에서는 성공 응답 코드로 201번을 보내줍니다.

204번은 요청이 성공은 했지만 응답할 콘텐츠가 없을 경우를 뜻합니다.
```