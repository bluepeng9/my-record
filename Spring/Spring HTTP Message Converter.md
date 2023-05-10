- 작성일: 2023-05-09
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

```
0 = ByteArrayHttpMessageConverter
1 = StringHttpMessageConverter
2 = MappingJackson2HttpMessageConverter
.
.
.
```

`HTTP Message Converter`는 HTTP 요청, HTTP 응답 둘 다에 사용됩니다.

스프링 부트는 다양한 메시지 컨버터를 제공하는데, 대상 클래스 타입과 미디어 타입 둘을 체크해서 사용여부를 결정합니다. 만약 조건을 만족하지 않으면 다음 메시지 컨버터로 우선순위가 넘어가게 됩니다.

---

# 중요한 컨버터들

다음은 몇 가지 중요한 컨버터 입니다.

## ByteArrayHttpMessageConverter

- 처리하는 클래스 타입
    - `byte[]`
- 미디어타입
    - `*/*` ,
- 요청 
    - e.g.
        - `@RequestBody byte[] data`
- 응답
    - e.g.
        - `@ResponseBody return byte[]`
        - 미디어타입은 `application/octet-stream` 이 됩니다.
        
## StringHttpMessageConverter

- 처리하는 클래스 타입
    - `String`
- 미디어타입
    - `*/*`
- 요청
    - e.g.
        - @RequestBody String data
- 응답
    - `@ResponseBody return "ok"`
    - 미디어타입은 `text/plain`이  됩니다.
    
## MappingJackson2HttpMessageConverter

- 처리하는 클래스 타입
    - 객체 또는 `HashMap`
- 미디어타입
    - `application/json` 관련
- 요청
    - e.g.
        - `@RequestBody HelloData data`
- 응답
    - e.g.
        - `@ResponseBody return helloData`
        - 미디어타입 `application/json` 관련

---
# HTTP 요청 데이터 읽기

1. 컨트롤러에서 `@RequestBody` , `HttpEntity` 파라미터를 사용한 컨트롤러에 HTTP 요청이 들어옵니다.
2. 메시지 컨버터가 메시지를 읽을 수 있는지 확인하기 위해 `canRead()` 를 호출합니다.
    - 대상 클래스 타입을 지원하는가.
        - e.g.
            - `@RequestBody` 의 대상 클래스 ( `byte[]` , `String` , `HelloData` )
    - HTTP 요청의 `Content-Type` 미디어 타입을 지원하는가.
        - e.g.
            - `text/plain` , `application/json` , `*/*`
3. `canRead()` 조건을 만족하면 `read()` 를 호출해서 객체를 생성하고, 반환합니다.

---
# HTTP 응답 데이터 생성

1.  컨트롤러에서 `@ResponseBody` , `HttpEntity` 로 값이 반환된다.
2. 메시지 컨버터가 메시지를 쓸 수 있는지 확인하기 위해 `canWrite()` 를 호출합니다.
    - 대상 클래스 타입을 지원하는가.
        - e.g.
            - return의 대상 클래스 (`byte[]` , `String` , `HelloData`)
    - HTTP 요청의 `Accept` 미디어 타입을 지원하는가.(더 정확히는 `@RequestMapping` 의 `produces`)
        - e.g.
            - `text/plain` , `application/json` , `*/*`
3. `canWrite()` 조건을 만족하면 `write()` 를 호출해서 HTTP 응답 메시지 바디에 데이터를 생성합니다.

---

# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)