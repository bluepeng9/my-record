- 작성일: 2023-05-09
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

쿼리 파라미터, 폼 파라미터, 요청에서 파일을 추출할 때도 사용할 수 있는 `@RequestParam` 어노테이션에 대해 알아보겠습니다.

---

# 기본

`id`라는 쿼리 파라미터를 받는 예시를 보겠습니다.

```java
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(@RequestParam String id) {
    return "ID: " + id;
}
```

`@RequestParam`을 통해 `id`를 추출할 수 있어, 다음과 같은 응답을 받을 수 있습니다.

```bash
http://localhost:8080/spring-mvc-basics/api/foos?id=abc
----
ID: abc
```

---
# 변수명과 파라미터의 이름이 다른 경우

이전 예제에서, 파라미터의 이름과 변수명이 같았습니다.

하지만 항상 이런 경우만 존재하진 않습니다.

다행히도 `@RequestParam`의 `name` 속성을 활용할 수 있습니다.

```java
@PostMapping("/api/foos")
@ResponseBody
public String addFoo(
    @RequestParam(name = "id") String fooId, // @RequestParam("id")도 가능
    @RequestParam String name
) { 
    return "ID: " + fooId + " Name: " + name;
}
```

파라미터 `id`의 값을 받아서 `fooID` 변수에 가져올 수 있습니다.

---

# 파라미터가 필수가 아닌 경우

기본적으로 `@RequestParam`가 붙은 메서드 파라미터는 필수적으로 요구됩니다.

즉, 만약 요청에 파라미터가 존재하지 않는다면 에러가 발생하게 됩니다.

```bash
GET /api/foos HTTP/1.1
-----
400 Bad Request
Required String parameter 'id' is not present
```

하지만 `required` 속성을 설정해서 이를 해결할 수 있습니다.

```java
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(@RequestParam(required = false) String id) { 
    return "ID: " + id;
}
```

이 경우 다음의 요청도,

```bash
http://localhost:8080/spring-mvc-basics/api/foos?id=abc
----
ID: abc
```

파라미터가 존재하지 않는 경우도

```bash
http://localhost:8080/spring-mvc-basics/api/foos
----
ID: null
```

정상적으로 수행할 수 있습니다.


## 주의할 점

- `primitive` 타입은 `null`이 될 수 없기 때문에 사용할 수 없습니다.
    - `Integer`과 같이 `null` 이 가능할 수 있도록 해야 합니다.
- `api/foos?username=` 와 같이 요청이 들어오면 `id` 값은 `null`이 아닌 `""`가 됩니다.

---

# 기본 값이 필요한 경우

기본 값이 필요하다면, `defaultValue` 속성을 통해 지정할 수 있습니다.

```java
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(
    @RequestParam(defaultValue = "test") String id
) {
    return "ID: " + id;
}
```

이 경우 유저가 파라미터를 제공하지 않아도 오류가 발생하지 않습니다.

```bash
http://localhost:8080/spring-mvc-basics/api/foos
----
ID: test
```

파라미터가 존재한다면 다음과 같은 응답을 받을 수 있습니다.

```bash
http://localhost:8080/spring-mvc-basics/api/foos?id=abc
----
ID: abc
```


## 주의할 점

- `required` 속성과는 다르게 `api/foos?username=` 와 같이 요청이 들어오면 `id`  값은 `""`가 아닌  `defaultValue` 값이 됩니다.

---
# 모든 파라미터 매핑이 필요한 경우

여러 변수를 만들지 않고 한 번에 매핑하고 싶다면, `Map`을 사용할 수 있습니다.

```java
@PostMapping("/api/foos")
@ResponseBody
public String updateFoos(
    @RequestParam Map<String,String> allParams
) {
    return "Parameters are " + allParams.entrySet();
}
```

다음과 같이 요청에서 보냈던 모든 파라미터를 응답으로 받을 수 있습니다.

```bash
curl -X POST -F 'name=abc' -F 'id=123' http://localhost:8080/spring-mvc-basics/api/foos
-----
Parameters are {[name=abc], [id=123]}
```

## 주의할 점

- 파라미터의 값이 여러개인 경우 `MultiValueMap`을 사용해야 합니다.

---

# 하나의 이름에 여러 값을 갖는 파라미터의 경우

하나의 `@RequestParam`은 여러 값을 가질 수 있습니다.

```java
@GetMapping("/api/foos")
@ResponseBody
public String getFoos(@RequestParam List<String> id) {
    return "IDs are " + id;
}
```

이 경우 Spring MVC는 다음과 같이 쉼표로 구분된 요청을 받아 처리할 수 있습니다.

```bash
http://localhost:8080/spring-mvc-basics/api/foos?id=1,2,3
----
IDs are [1,2,3]
```

분리되어 있는 요청도 처리 가능합니다.

```bash
http://localhost:8080/spring-mvc-basics/api/foos?id=1&id=2
----
IDs are [1,2]
```

---

# Reference

- [Spring @RequestParam Annotation | Baeldung](https://www.baeldung.com/spring-request-param)
- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)