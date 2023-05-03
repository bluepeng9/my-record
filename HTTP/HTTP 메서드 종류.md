- 작성일: 2023-05-02
- 태그: 
- 분류
	- [HTTP 메서드](HTTP%20메서드.md)
- 관련 노트
---
# GET

```HTTP
GET /test/demo_form.php?name1=value1&name2=value2 HTTP/1.1
Host:www.example.com
```

- 리소스를 조회합니다.
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달합니다.
- Message body를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않습니다.

```text
Client                        Server
   |                           |
   | GET /api/data HTTP/1.1    |
   | Host: example.com         |
   | Accept: application/json  |
   | ------------------->      |                               
   |                           | HTTP/1.1 200 OK
   |    <----------------------| Content-Type: application/json
   |                           | Content-Length: 123
   |                           |
   |                           | {"foo": "bar", "baz": "far"}
   |                           |
```

---
# POST

```text
  Client                                 Server  
    |                                     |
    |  POST /test/demo_form.php HTTP/1.1  |
    |  Host: example.com                  |
    |  Content-Type: application/json     |
    |  Content-Length: 44                 |
    |                                     |
    |  {"name1":"value1","name2":"value2"}|
    +------------------------------>      |
    |                                     |
    |  HTTP/1.1 200 OK                    |
    |  Content-Type: application/json     |
    |  Content-Length: 44                 |
    |                                     |
    |  {"name1":"value1","name2":"value2"}|
    |      <------------------------------+
    |                                     |
```

- 요청 데이터를 처리합니다.
- Message body를 통해 서버로 요청 데이터를 전달합니다.
- 서버는 요청데이터를 처리합니다.
	- 주로 신규 리소스 등록, 프로세스 처리에 활용합니다. 
		- e.g. 주문에서 결제완료 -> 배달시작 -> 배달완료 처럼 단순히 값 변경을 넘어 프로세스의 상태가 변경되는 경우
- 다른 메서드로 처리하기 어려운 경우(애매한 경우) 사용하기도 합니다.
	- e.g. JSON으로 조회 데이터를 넘겨야 하는데, GET메서드를 사용하기 어려운 경우

---
# PUT

- 리소스를 대체합니다.
	- 만약 리소스가 없다면 생성합니다.
- 클라이언트가 리소스의 위치를 알고 URI를 지정합니다.
    - POST와의 차이점 입니다.
    - e.g.
        - 파일 등록 시 PUT /files/star.jpg . 이 경우 클라이언트가 리소스의 URI를 알고 관리합니다.

다음은 리소스가 대체되는 과정입니다.

```
  Client                              Server  
    |                                  |
    |  PUT /members/100 HTTP/1.1       |
    |  Host: example.com               |
    |  Content-Type: application/json  |
    |  Content-Length: 44              |
    |                                  |
    |  {"age":50}                      |
    |------------------------------>   |
    |                                  |

In server:

{"username":"old","age":51} -> {"age":50}
```

---
# Patch

- 리소스를 부분 변경합니다.

다음은 리소스가 부분 변경되는 과정입니다.

```
  Client                              Server  
    |                                  |
    |  Patch /members/100 HTTP/1.1     |
    |  Host: example.com               |
    |  Content-Type: application/json  |
    |  Content-Length: 44              |
    |                                  |
    |  {"age":50}                      |
    |------------------------------>   |
    |                                  |

In server:

{"username":"old","age":51} -> {"username":"old","age":50}
```

---

# Delete

- 리소스를 제거합니다.

다음은 리소스가 제거되는 과정입니다.

```
  Client                              Server  
    |                                  |
    |  Delete /members/100 HTTP/1.1    |
    |  Host: example.com               |
    |------------------------------>   |
    |                                  |

In server:

{"username":"old","age":51} -> X
```

---
# Reference

- 