- 작성일: 2023-04-25
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트
---

> RequestBody와 ResponseBody 어노테이션에 대해 알아보겠습니다.
>```java
>@PostMapping
>public HttpStatus something (@RequestBody MyModel myModel) {
>  return HttpStatus.OK;
>}
>```

---
# @RequestBody

간단히 말해서 @RequestBody 어노테이션은 HttpRequest body를  transfer 객체 또는 domain 객체에 매핑하여, HttpRequest의 body를 자바 객체로 자동으로 역직렬화 할 수 있도록 합니다.

```java
@PostMapping("/request")
public ResponseEntity postController(@RequestBody LoginForm loginForm) {
    exampleService.fakeAuthenticate(loginForm);
    return ResponseEntity.ok(HttpStatus.OK);
}
```

RequestBody 어노테이션과 같이 기술한 Type은 반드시 클라이언트에서 보내온 JSON과 일치해야 합니다.

## 주의

- 생략이 불가능합니다.
    - `@ModelAttribute` 혹은 `@RequestParam` 이 적용되기 때문입니다.

---

# @ResponseBody


ResponseBody 어노테이션은 Controller에게, return된 객체가 자동으로 JSON으로 변환되어 다시 HttpResponse 객체로 전달된다고 알려줍니다. 

다음과 같은 특징을 가지고 있습니다.

- HTTP의 BODY에 문자 내용을 직접 반환 합니다.
- `viewResolver`  대신 `HttpMessageConverter`가 동작합니다.
- 기본 문자 처리는 `StringHttpMessageConverter`가 담당합니다.
- 기본 객체 처리는 `MappingJackson2HttpMessageConverter`가 담당합니다.
- `byte` 처리 등등 기타 여러 `HttpMessageConverter`가 기본적으로 등록되어 있습니다.
  
Response 객체가 하나 있다고 가정해보겠습니다.

```java
public class ResponseTransfer {
    private String text; 
    
    // getter 와 setter ...
}
```

다음으로 예시와 같은 Controller가 있을 수 있습니다.

```java
@Controller
@RequestMapping("/post")
public class ExamplePostController {

    @PostMapping("/response")
    @ResponseBody
    public ResponseTransfer postResponseController(
      @RequestBody LoginForm loginForm) {
        return new ResponseTransfer("Thanks For Posting!!!");
     }
}
```

Postman과 같은 툴로 테스트를 해봤을 때 다음과 같은 response를 받을 수 있습니다.

```json
{"text":"Thanks For Posting!!!"}
```

## @RestController

@RestController 어노테이션을 붙였다면, 스프링이 이와 같은 일을 자동으로 해주기 때문에 @ResponseBody와 같은 어노테이션을 수동으로 붙일 필요는 없습니다.

---
# 출처

- [Spring's RequestBody and ResponseBody Annotations | Baeldung](https://www.baeldung.com/spring-request-response-body)
---
# 관련 링크