- 작성일: 2023-05-09
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트
    - [Spring @RequestBody, @ResponseBody Annotations](Spring%20@RequestBody,%20@ResponseBody%20Annotations.md)

---

```java
@PostMapping("/request-body-string-v3")  
public HttpEntity<String> requestBodyStringV3(
    HttpEntity<String> httpEntity
) throws IOException {  

    String messageBody = httpEntity.getBody();  
      
    log.info("messageBody={}", messageBody);  
      
    return new HttpEntity<>("ok");  
}
```

다음과 같은 특징이 있습니다.

- HTTP header, body 정보를 편리하게 조회할 수 있습니다.
- 요청 파라미터를 조회하는 기능과는 관계 없습니다.
    - `@RequestParam` X, `@ModelAttribute` X
- HttpEntity는 응답에도 사용 가능합니다.
    - 메시지 바디 정보를 직접 반환할 수 있습니다.
    - 헤더 정보를 포함할 수 있습니다.
    - 이 때 view 조회는 일어나지 않습니다.


`HttpEntity`를 상속받은 다음 객체들도 같은 기능을 제공합니다.

# RequestEntity

- HTTPMethod, url 정보가 추가 되었습니다.
- 요청에서 사용합니다.

# ResponseEntity

- HTTP 상태 코드를 설정할 수 있습니다.
- 응답에서 사용합니다.


---

# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)