- 작성일: 2023-05-08
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

```java
log.trace("trace log{}=" + name); // 1

log.trace("trace log= {}", name); // 2
```

두 로그는 보기에 똑같이 작동합니다. 하지만 1번 로그는 `String`을 합치는 연산이 일어나고 `method`에 전달되는 반면, 2번 로그는 각 `argument`가 연산없이 `method`로 전달됩니다.

따라서 2번과 같이 코드를 작성해야 합니다.

---

# Reference

- 