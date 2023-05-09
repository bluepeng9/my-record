- 작성일: 2023-05-09
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

# Method-argument level

스프링MVC는 `@ModelAttribute` 가 있으면 다음을 실행합니다.

- `@ModelAttribute`가 붙은 객체(여기선 `HelloData`)를 생성합니다.
- 요청 파라미터의 이름으로 `HelloData` 객체의 프로퍼티를 찾습니다.
    - 객체에 getUsername() , setUsername() 메서드가 있으면, 이 객체는 username 이라는 프로퍼티를 가지고 있습니다. username 프로퍼티의 값을 변경하면 setUsername() 이 호출되고, 조회하면 getUsername() 이 호출된다
- 그리고 해당 프로퍼티의 `setter`를 호출해서 파라미터의 값을 입력(바인딩) 한다.
    - 예) 파라미터 이름이 username 이면 setUsername() 메서드를 찾아서 호출하면서 값을 입력합니다.

`age = abc` 처럼 숫자가 들어가야 할 곳에 문자를 넣으면 BindException 이 발생합니다.

## 생략 가능

`@ModelAttribute`는 생략이 가능합니다. 스프링은 해당 생략시 다음과 같은 규칙을 적용합니다.

- String , int , Integer 같은 단순 타입 = `@RequestParam`
- 나머지 = `@ModelAttribute` (argument resolver 로 지정해둔 타입 외)


---

# Reference

- [Web on Servlet Stack (spring.io)](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-modelattrib-method-args)
- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)