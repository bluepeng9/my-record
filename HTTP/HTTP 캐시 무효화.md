- 작성일: 2023-05-04
- 태그: 
- 분류
    - [HTTP 캐시](HTTP%20캐시.md)
- 관련 노트
---

```HTTP
Cache-Control: no-cache, no-store, must-revalidate
Pragma: no-cache
```

캐시 무효화에 대해 알아보겠습니다.

---
# 필요성

캐시를 적용하지 않아도, 웹 브라우저가 임의로 캐시를 하는 경우가 있습니다. 이를 예방하기 위해 캐시 무효화를 사용합니다.

---

# Cache-Control

다음은 캐시 무효화에 사용 되는 헤더 정보입니다.

- `Cache-Control: no-cache`
    - 데이터는 캐시해도 되지만, 항상 origin 서버에 검증한 이후 사용해야 합니다.
- `Cache-Control: no-store`
    - 데이터에 민감한 정보가 있으므로 저장하면 안됨
        - 메모리에서 사용하고 최대한 빨리 삭제해야 합니다.
- `Cache-Control: must-revalidate`
    - 캐시 만료후 최초 조회시 origin 서버에 검증해야 합니다.
    - 원 서버 접근 실패시 반드시 오류가 발생해야합니다. - 504(Gateway Timeout)
    - 유효 시간이라면 캐시를 사용함
- `Pragma: no-cache`
    - HTTP 1.0 하위 호환을 위해 사용합니다.

---

# no-cache vs must-revalidate

- 캐시 서버에 접근할 수 없는 경우
    - `no-cache`
        - origin 서버에 접근 할 수 없는 경우 캐시서버 설정에 따라 캐시 데이터를 반환할 수 있습니다.
    - `must-revalidate`
        - origin 서버에 접근 할 수 없는 경우 항상 오류(504)가 발생해야 합니다.

---

# Reference

- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)