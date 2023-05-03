- 작성일: 2023-05-02
- 태그: 
- 분류
	- [HTTP](HTTP.md)
- 관련 노트
---

# Index

- [HTTP 메서드](HTTP%20메서드.md)

---

# Request Message

Request Message는 다음과 같은 구조를 가지고 있습니다.

```
GET /index.html HTTP/1.1           // start line (request-line)
Host: www.example.com              // headers
User-Agent: Mozilla/5.0            
Content-Type: application/json     
                                   // empty line
{"name":"Alice","age":25}          // body
```

## Start Line

### HTTP 메서드

- 종류 `GET`, `POST`, `PUT`, `DELETE` ...
- 서버가 수행해야 할 동작 지정
	- `GET`
		- 리소스 조회
	- `POST`
		- 요청내역 처리

### 요청 대상

- absolute-path\[?query\] (절대경로\[?쿼리\])

### HTTP 버전

- e.g. `HTTP/1.1`

---

# Response Message

Response Message는 다음과 같은 구조를 가지고 있습니다.

```
HTTP/1.1 200 OK                        // start line (status-line)
Content-Type: text/html; charset=UTF-8 // headers
Content-Length: 138
                                       // empty line
<html>                                 // body
<head>
<title>Example</title>
</head>
<body>
<h1>Hello, world!</h1>
</body>
</html>
```

## Start line

### HTTP 버전

- e.g.  `HTTP/1.1`

### HTTP 상태 코드

요청 성공, 실패를 나타냅니다.

- 200
	- 성공
- 400
	- 클라이언트 요청 오류
- 500
	- 서버 내부 오류
### 이유 문구

사람이 이해할 수 있는 짧은 상태 코드 설명 글

## HTTP 헤더

HTTP 전송에 필요한 모든 부가정보를 담고 있습니다.

- e.g. message body의 내용, message body의 크기...

구조는 다음과 같습니다.

- header-field
- field-name
	- Host 띄어쓰기 : 안 됨 -> Host:
	- 대소문자 구분 없음
- OWS field-value OWS
	- 대소문자 구분

다음과 같은 특징이 있습니다.

- 필요 시 임의의 헤더 추가 가능

## HTTP 메시지 바디

다음과 같은 특징이 있습니다.

- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능



---
# Reference

- [HTTP Messages - HTTP | MDN (mozilla.org)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC) 