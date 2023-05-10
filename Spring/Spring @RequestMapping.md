- 작성일: 2023-05-08
- 태그: #작성중 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

# method

매핑할 `HTTP method`를 지정해 매핑의 범위를 제한시킬 수 있습니다.

다음은 `GET` 메서드로만 제한시킨 예시입니다.

```java
@RequestMapping(value = "/hello-basic", method = RequestMethod.GET)  
public String helloBasic() {  
    log.info("helloBasic");
    return "ok";
}
```

---
# params

`params`를 사용해서, request mapping의 범위를 좁힐 수 있습니다. 다음 예시는 같은 `URL`에 여러 `handler`를 가진 경우 입니다.

```java
@RestController
@RequestMapping("/home")
public class IndexController {

    @RequestMapping(value = "/fetch", params = {
        "personId=10"
    })
    String getParams(@RequestParam("personId") String id) {
        return "Fetched parameter using params attribute = " + id;
    }

    @RequestMapping(value = "/fetch", params = {
        "personId=20"
    })
    String getParamsDifferent(@RequestParam("personId") String id) {
        return "Fetched parameter using params attribute = " + id;
    }
}
```

`URL`이 만약 `/home/fetch?id=10` 이라면 `getParams` 핸들러가 동작합니다. `/home/fetch?personId=20`  `URL`로 요청이 온다면 `getParamsDifferent` 핸들러 메서드가 동작하게 됩니다.

---

# header

```java
/**  
* 특정 헤더로 추가 매핑  
* headers="mode", 헤더의 key 값에 mode가 있는 경우
* headers="!mode" 헤더의 key 값에 mode가 없는 경우
* headers="mode=debug" 헤더에 mode=debug key value가 존재하는 경우
* headers="mode!=debug" (! = ) 헤더에 mode=debug key value가 존재하지 않는 경우
*/  
@GetMapping(value = "/mapping-header", headers = "mode=debug")  
public String mappingHeader() {  
    log.info("mappingHeader");  
    return "ok";  
}
```

헤더에 조건을 걸 수 있습니다. 만약 미디어 타입 헤더에 조건을 걸고 싶다면, 스프링 내부적으로 처리하는 방식이 있기 때문에 `consumes`를 사용해야 합니다.

---

# consumes

```java
/**  
* Content-Type 헤더 기반 추가 매핑 Media Type  
* consumes="application/json"
* consumes="!application/json"
* consumes="application/*"
* consumes="*\/*"
* MediaType.APPLICATION_JSON_VALUE  application/json 과 같은 값
*/  
@PostMapping(value = "/mapping-consume", consumes = "application/json")  
public String mappingConsumes() {  
    log.info("mappingConsumes");  
    return "ok";  
}
```

`Content-Type`에 조건을 걸 수 있습니다.

---
# produces

```java
/**  
* Accept 헤더 기반 Media Type
* produces = "text/html"
* produces = "!text/html"  
* produces = "text/*"  
* produces = "*\/*"  
*/  
@PostMapping(value = "/mapping-produce", produces = "text/html")  
public String mappingProduces() {  
    log.info("mappingProduces");  
    return "ok";  
}
```

`Accept`헤더가 `produces`의 값을 포함하고 있다면 실행됩니다. 만약 맞는 핸들러가 메서드가 없다면 `406 Not acceptable` 에러가 발생됩니다.

---

# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)
- [Using the Spring @RequestMapping Annotation - DZone](https://dzone.com/articles/using-the-spring-requestmapping-annotation#:~:text=The%20params%20element%20of%20the,define%20params%20as%20myParams%20%3D%20myValue.)
- [HeadersRequestCondition (Spring Framework 6.0.8 API)](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/servlet/mvc/condition/HeadersRequestCondition.html)