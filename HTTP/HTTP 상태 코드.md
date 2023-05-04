- 작성일: 2023-05-03
- 태그: 
- 분류
    - [HTTP](HTTP.md)
- 관련 노트
---

```
+-----------------+-----------------+-----------------+
| 1xx Information | 2xx Success     | 3xx Redirection |
+-----------------+-----------------+-----------------+
| 100 Continue    | 200 OK          | 300 Multiple    |
| 101 Switching   | 201 Created     |     Choices     |
|     Protocols   | 202 Accepted    | 301 Moved       |
| 102 Processing  | 203 Non Author- |     Permanently |
|                 |     itative     | 302 Found       |
|                 |     Information | 302 Found       |
|                 | 204 No Content  | 303 See Other   |
|                 | 205 Reset       | 304 Not Modified|
|                 |     Content     | 305 Use Proxy   |
|                 | 206 Partial     | 306 Switch Proxy|
|                 |     Content     | 307 Temporary   |
|                 |                 |     Redirect    |
+-----------------+-----------------+-----------------+
| 4xx Client Error| 5xx Server Error|                 |
+-----------------+-----------------+-----------------+
| 400 Bad Request | 500 Internal    |                 |
| 401 Unauthorized|     Server Error|                 |
| 402 Payment     | 501 Not         |                 |
|     Required    |     Implemented |                 |
| 403 Forbidden   | 502 Bad Gateway |                 |
| 404 Not Found   | 503 Service     |                 |
| 405 Method Not  |     Unavailable |                 |
|     Allowed     | 504 Gateway     |                 |
| ...             |     Timeout     |                 |
+-----------------+-----------------+-----------------+
```

HTTP 상태 코드에  대해 알아보겠습니다.

---

# 1xx (informational)

요청이 수신되어 처리중임을 알려줍니다.

---

# 2xx (Successful)

요청이 정상 처리되었음을 알려줍니다.

- 201 Created
    - 요청이 성공하여 새로운 리소스가 생성됩니다.
        - 생성된 리소스는 Location 헤더 필드로 식별 가능합니다.
- 202 Accepted
    - 요청이 접수되었으나 처리가 완료되지 않았습니다.
    - e.g.
        - 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함
- 204 No Content
    - 서버가 요청을 성공적으로 수행했으나 응답 페이로드 본문에 보낼 데이터가 없습니다.
    - 결과 내용이 없어도 204 메시지(2xx)만으로 성공을 인식할 수 있습니다.
    - e.g.
        - 웹 문서 편집기의 save 버튼의 결과로 아무 내용이 없어도 됩니다.
        - 웹 문서 편집기의 save 버튼을 눌러도 같은 화면을 유지해야 합니다.

---

# 3xx (Redirection)


요청을 완료하려면 추가 행동이 필요함을 알려줍니다. 웹 브라우저는 3xx의 응답 결과에 Location 헤더가 있으면, Location 위치로 자동 이동합니다.

## 영구 리다이렉션

```
   Client                Server                New URL    
     |                     |                     |
     | GET /index.php      |                     |
     |-------------------->|                     |
     |                     |                     |
     | 301 Moved           |                     |
     | Location: /index.asp|                     |
     |<--------------------|                     |
     |                     |                     |
     | GET /index.asp      |                     |
     |------------------------------------------>|
     |                     |                     |
     | 200 OK              |                     |
     |<------------------------------------------|
```

- 특정 리소스의 URI가 영구적으로 이동했음을 알려줍니다.
- 원래의 URL을 사용하지 않습니다.
- 검색 엔진 등에서도 변경을 인지할 수 있습니다.
- 301 Moved Permanently
    - 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있습니다.(MAY)
- 308 Permanent redirect
    - 301과 기능은 같습니다.
    - 리다이렉트시 요청 메서드와 본문을 유지합니다.(처음 POST를 보내면 리다이렉트도 POST 사용)
- e.g.
    - /members -> /users
    - /event -> /new-event

## 일시 리다이렉션

- 302 FOUND
    - 리다이렉트 시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있습니다.(MAY)
- 307 Temporary Redirect
    - 302와 기능은 같습니다.
    - 리다이렉트시 요청 메서드와 분문을 유지합니다.(MUST)
- 303 See Other
    - 302와 기능은 같습니다.
    - 리다이렉트 시 요청 메서드가 GET으로 변경됩니다.
- e.g.
    - 주문 완료 후 주문 내역 화면으로 이동
    - PRG


### PRG (Post/Redirect/GET)

POST로 주문 후 웹 브라우저를 새로고침하면 새로고침은 다시 요청을 의미하기 때문에 다음과 같이 중복 주문이 될 수 있습니다.

```
+--------+    POST    +--------+
| Client | ---------> | Server |
+--------+            +--------+
  ^  ^                   |  |
  |  |                   |  |
  |  +-------------------+  |
  |     Form submission     |
  +-------------------------+
     Page reload or share
```

Redirection을 이용해 중복 주문을 막을 수 있습니다.

```
                        302 or 303
+------+  POST  +------+ Redirect +------+  GET   +------+
|Client| -----> |Server| -------> |Client| -----> |Server|
+------+        +------+          +------+        +------+
```



## 특수 리다이렉션

- 300 Multiple Choices
        - 사용하지 않습니다.
- 304 Not modified
    - 캐시를 목적으로 사용합니다.
    - 결과 대신 캐시를 사용합니다.
    - 304 응답은 응답에 Message body를 포함하면 안 됩니다.
        - 캐시를 사용해야 하기 때문입니다.
    - 조건부 GET, HEAD 요청시 사용합니다.

---

# 4xx (Client Error)

- 클라이언트 오류로, 잘못된 문법등으로 서버가 요청을 수행할 수 없음을 알려줍니다.
- 오류의 원인이 클라이언트에 있습니다.
- 클라이언트가 이미 잘못된 요청, 데이터를 보내고 있기 때문에, 똑같은 재시도가 실패합니다.

다음은 Client Error의 종류입니다.

- 400 BAD Request
    - 요청 구문, 메시지 등등의 오류
    - 클라이언트는 요청 내용을 다시 검토하고 보내야 합니다.
    - e.g.
        - 요청 파라미터가 잘못된 경우
        - API 스펙이 맞지 않는 경우
- 401 Unauthorized
    - 인증되지 않은 경우를 의미합니다.
    - 오류 발생 시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명합니다.
    - 참고
        - 인증(Authentication)
            - 본인이 누구인지 확인, (로그인)
        - 인가(Authorization)
            - Admin 권한처럼 특정 리소스에 접근할 수 있는 권한을 부여합니다.
            - 인증이 있어야 권한이 있습니다.
- 403 Forbidden
    - 서버가 요청을 이해했지만 승인을 거부한 경우입니다.
    - 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우를 의미합니다.
    - e.g.
        - Admin 등급이 아닌 사용자가 로그인은 했지만, Admin 등급의 리소스에 접근하는 경우
- 404 Not Found
    - 요청 리소스가 서버에 없는 경우를 의미합니다.
    - 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을때 역시 사용가능합니다.

---

# 5xx (Server Error)

- 서버 오류로, 서버가 정상 요청을 처리하지 못했음을 알려줍니다.
- 서버에 문제가 있기 때문에 재시도 하면 성공할 수도 있습니다.

---

# 만약 모르는 상태코드가 나타난다면

클라이언트는 상위 상태코드로 해석해서 처리하면 됩니다. 따라서 미래에 새로운 상태코드가 추가되어도 클라이언트를 변경하지 않아도 됩니다.

- e.g.
- 299 ??? -> 2xx (Successful)
- 451 ??? -> 4xx (Client Error)
- 599 ??? -> 5xx (Server Error)

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)