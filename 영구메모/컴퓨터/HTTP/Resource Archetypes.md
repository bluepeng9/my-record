- 작성일: 2023-05-03
- 태그: 
- 분류
    - [HTTP](HTTP.md)
- 관련 노트
---

```
Resource Archetypes
|
+-- Document
|
+-- Collection
|
+-- Store
|
+-- Controller
```

좋은 API 설계를 위해 Resource 전형을 4가지로 분류해 알아보겠습니다.

---
# Document

>http://api.example.com/device-management/managed-devices/{device-id}
>
>http://api.example.com/user-management/users/{id}
>
>http://api.example.com/user-management/users/admin

- 인스턴스 하나, 데이터베이스의 row와 같은 단일 개념입니다.
- REST 에서는 Document를 Collection 내의 단일 리소스로 볼 수 있습니다. 
- 일반적으로 document의 상태를 표현할 때 다른 resource에 대한 링크와 값 모두가 포함됩니다.
    - e.g. 강아지 사진에 대한 document는 같은 강아지의 다른 사진이나 주인의 사진 또는 강아지에 관한 웹사이트에 대한 링크가 포함될 수 있습니다.

---

# Collection

>  http://api.example.com/device-management/managed-devices
>  
> http://api.example.com/user-management/users
> 
> http://api.example.com/user-management/users/{id}/accounts
> 

- 서버가 관리하는 리소스 디렉터리입니다.
- 서버가 리소스의 URI를 생성하고 관리합니다.
- Client는 서버에게 Collection에 추가할 새 리소스를 제안할 수 있습니다.
    - 그러나 새 리소스를 만들지는 Collection의 설정에 달려있습니다.
- 복수형을 사용해 나타냅니다.

---

# Store

> http://api.example.com/song-management/users/{id}/playlists

- Client가 관리하는 리소스 저장소입니다.
- Client가 리소스를 넣고, 꺼내고, 삭제할 시기를 결정할 수 있습니다.
- 새 URI를 생성하지 않습니다.
    - 대신 저장된 각 리소스에는 클라이언트가 선택한 URI가 있습니다.
- 나타낼 때 복수형을 사용합니다.



---
# Controller

> http://api.example.com/cart-management/users/{id}/cart/checkout
> 
> http://api.example.com/song-management/users/{id}/playlist/play

- 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스를 실행합니다.
- 동사를 사용해 나타냅니다.

---
# Reference

- [REST API - URL Naming Conventions (restfulapi.net)](https://restfulapi.net/resource-naming/)
- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)