- 작성일: 2023-05-04
- 태그: 
- 분류
    - [HTTP 메시지](HTTP%20메시지.md)
- 관련 노트
    - [HTTP 상태 코드](HTTP%20상태%20코드.md)
---

```
HTTP header 특별한 정보
|
+-- Host
|
+-- Location
|
+-- Allow
|
+-- Retry-After
```

특별한 정보를 제공하는 HTTP header를 알아보겠습니다.

---

# Host

요청한 호스트(도메인)의 정보를 나타냅니다.

다음과 같은 특징을 가집니다.

- 요청에서 사용합니다.
- 필수입니다.
- 다음과 같은 경우 사용합니다.
    - 하나의 서버가 여러 도메인을 처리해야 할 때
    - 하나의 IP 주소에 여러 도메인이 적용되어 있을 때

---

# Location

리다이렉트할 페이지를 가리킵니다.

다음과 같은 특징을 가집니다.

- 상태코드 201의 Location은 요청에 의해 생성된 리소스의 URI를 나타냅니다.
- 상태코드 301의 Location은 리디렉션하기 위핸 대상 리소스를 가리킵니다.

---
# Allow

허용 가능한 HTTP 메서드를 나타냅니다.

다음과 같은 특징을 가집니다.

- 405 응답(Method Not Allowed)에서 포함되어야 합니다.
- e.g.
    - Allow: GET, HEAD, PUT

# Retry-After

유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간을 나타냅니다.

다음과 같은 특징을 가집니다.

- 503 (Service Unavailable) 응답에서 서비스가 언제까지 불능인지 알려줄 수 있습니다.
- 날짜 표기 또는 초 단위 표기가 가능합니다.


---

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)