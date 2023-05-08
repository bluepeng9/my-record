- 작성일: 2023-05-08
- 태그: #작성중 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

# Params

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

# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)
- [Using the Spring @RequestMapping Annotation - DZone](https://dzone.com/articles/using-the-spring-requestmapping-annotation#:~:text=The%20params%20element%20of%20the,define%20params%20as%20myParams%20%3D%20myValue.)