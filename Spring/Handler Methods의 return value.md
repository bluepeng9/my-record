- 작성일: 2023-05-08
- 태그: #작성중 
- 분류
    - [Spring](Spring.md)
- 관련 노트
    - [Spring @RequestBody, @ResponseBody Annotations](Spring%20@RequestBody,%20@ResponseBody%20Annotations.md)
---

# String

>   A view name to be resolved with `ViewResolver` implementations and used together with the implicit model — determined through command objects and `@ModelAttribute` methods. The handler method can also programmatically enrich the model by declaring a `Model` argument

Handler 메서드가 String을 반환하면, `ViewResolver`의 구현체가 이를 처리합니다. `Model argument`를 활용하여 데이터를 전달해줄 수도 있습니다. 

# ModelAndView

```java
@RequestMapping("/response-view-v1")  
public ModelAndView responseViewV1() {  

    ModelAndView mav = new ModelAndView("response/hello")
    .addObject("data", "hello!");  
      
    return mav;  
}
```

> The view and model attributes to use and, optionally, a response status.

`view`와 `model attribute` 를 제공합니다. 추가적으로 `response status`를 제공할 수도 있습니다.

---

# Reference

- [Web on Servlet Stack (spring.io)](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-return-types)