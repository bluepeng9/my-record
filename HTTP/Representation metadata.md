- 작성일: 2023-05-03
- 태그: 
- 분류
    - [HTTP Representation](HTTP%20Representation.md)
- 관련 노트
---

```
Representation Metatdata
|
+-- Content-Type
|
+-- Content-Encoding
|
+-- Content-Language
|
+-- Content-Location
```

```HTTP
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Encoding: gzip
Content-Length: 3423

<html>
    <body>...</body>
</html>
```


Representation metadata 4가지에 대해 알아보겠습니다.

---

# Content-Type (표현 데이터의 형식 설명)

- 미디어 타입, 문자 인코딩 정보를 알려줍니다.
- e.g.
    - text/html; charset=utf-8
    - application/json
    - image/png

---

# Content-Encoding (표현 데이터 인코딩)

- 표현 데이터를 압축하기 위해 사용합니다.
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더를 추가합니다.
- 데이터를 읽는 쪽에서는 인코딩 헤더의 정보로 압축을 해제합니다.
- e.g.
    - gzip
    - deflat
    - identity

---

# Content-Language (표현 데이터의 자연 언어)

- 표현 데이터의 자연 언어를 표현합니다.
- e.g.
    - ko
    - en
    - en-US

---

# Content-Length (표현 데이터의 길이)

- 바이트 단위입니다.
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안 됩니다.



---

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC) 