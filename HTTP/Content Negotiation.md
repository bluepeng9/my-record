- 작성일: 2023-05-04
- 태그: 
- 분류
    - [HTTP 메시지](HTTP%20메시지.md)
- 관련 노트
---

```
Content Negotiation
|
+-- Accept
|
+-- Accept-CharSet
|
+-- Accept-Encoding
|
+-- Accept-Language
```

Content Negotiation(협상)에 대해 알아보겠습니다.

---

# Header의 종류

- Accept
    - 클라이언트가 선호하는 미디어 타입을 전달합니다.
- Accept-Charset
    - 클라이언트가 선호하는 문자 인코딩을 전달합니다.
- Accept-Encoding
    - 클라이언트가 선호하는 압축 인코딩을 전달합니다.
- Accept Language
    - 클라이언트가 선호하는 자연 언어를 전달합니다.

`Header`는 위 처럼 4가지가 존재하고, 요청 시에만 사용합니다.

---
# Quality Values(q)

- 어떤 언어를 고를지 결정하기 위해 Quality Values(q) 값을 사용합니다
    - 생략 시 1로 간주합니다.
- 구체적인 것을 우선적으로 선택합니다.
    - e.g.
        - Accept: text/*, text/plain, text/plain;format=flowed, \*/\*
            1. text/plain;format=flowed
            2. text/plain
            3. text/*
            4. \*/\*
---
# 적용 예시

다음은 독일어와 영어를 지원하는 서버의 예시입니다.

```text
Browser                                  Server
   |                                        |
   | Accept-Language                        |
   | (ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7)  |
   |------------------------------------>   |
   |                                        |-- select best match 
   |                                        |   (ko-KR)           
   |                    Content-Language    |
   |                    (en)                |
   |   <------------------------------------|
   |                                        |
```

한국어 다음으로 영어가 우선순위가 높기 때문에 영어가 선택되었습니다.

---

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 대시보드 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)