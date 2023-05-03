- 작성일: 2023-05-03
- 태그: 
- 분류
    - [HTTP 메시지](HTTP%20메시지.md)
- 관련 노트
---

HTTP 헤더의 특징은 다음과 같습니다.

- HTTP 전송에 필요한 모든 부가정보를 담고 있습니다.
    - e.g.
        - 메시지 바디의 내용
        - 메시지 바디의 크기
        - 압축
- 필요시 임의의 헤더를 추가할 수 있습니다.

과거의 RFC2616에 따라 분류한 헤더는 다음과 같습니다.

- General Header
    - 메시지 전체에 적용되는 정보
        - e.g.
            - connection: close
- Request Header
    - 요청 정보
        - e.g.
            - User-Agent: Mozilla/5.0 (Macintosh; ..)
- Response Header
    - 응답 정보
        - e.g.
            - Server: Apache
- Entity Header
    - 엔티티 본문 (`<html> ... </html>`)의 데이터를 해석할 수 있는 정보를 제공합니다.
        - e.g.
            - Content-Type: text/html, Content-Length: 3423

하지만 RFC 2616이 폐기되면서 용어의 변화가 생겼습니다.

- 엔티티(Entity) -> 표현(Representation)
- 표현 = 표현 메타데이터 + 표현 데이터

다음은 RFC7230에서 정의한 용어입니다.

- 메시지 본문을 통해 표현 데이터를 전달합니다.
- 메시지 본문 = Payload
- 표현은 요청이나 응답에서 전달할 실제 데이터를 의미합니다.
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보를 제공합니다.
    - e.g.
        - 데이터 유형(html, json), 데이터 길이, 압축 정보 등

---

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)