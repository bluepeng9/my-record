- 작성일: 2023-05-05
- 태그: 
- 분류
    - [JAVA](JAVA.md)
- 관련 노트
    - [Web Server와 Web Application Server](../Spring/Web%20Server와%20Web%20Application%20Server.md)
---

# 정의

자바 기반 Web Application 프로그래밍 기술로, 동적 웹 페이지를 만들 수 있게 해줍니다.

---

# 특징

```java
@WebServlet(name = "hellowServlet", urlPatterns = "/hello")  
class HelloServlet extends HttpServlet {  
  
    @Override  
    protected void service(
        HttpServletRequest request,
        HttpServletResponse response
    ) {  
        //애플리케이션 로직  
    }  
}
```

다음은 서블릿의 특징입니다.

-   urlPatterns(/hello)의 URL이 호출되면 서블릿 코드가 실행됩니다.
-   HttpServletRequest로 인해 HTTP 요청 정보를 편리하게 사용할 수 있습니다.
-   HttpServletResponse로 인해 HTTP 응답 정보를 편리하게 제공할 수 있습니다.

---

# 작동 흐름

```
+-------------+      +-----------------+      +----------+
|   Client    |----->|  Web Application|----->| Servlet  |
|             |<-----|    Server       |<-----| Container|
+-------------+      +-----------------+      +----------+
```

- 브라우저와 같은 Client가 `localhost:8080/hello` 와 같은 주소로 request를 보냅니다.
- `WAS`는 `Request`, `Response` 객체를 새로 만들고 `helloServlet`을 실행합니다.
- return 값을 바탕으로 http response message를 만들어 Client에게 전달합니다.

---
# Servlet Container

`Tomcat`처럼 `Servlet`을 지원하는 `WAS`를 서블릿 컨테이너라고 합니다.

다음과 같은 기능을 합니다.

-   서블릿 컨테이너는 서블릿 객체의 생명 주기를 관리합니다.
    - e.g.
        - 생성, 초기화, 호출, 종료
-   서블릿 객체는 싱글톤으로 관리
    -   고객의 요청이 올 때 마다 계속 객체를 생성하는 것은 비효율적이기 때문입니다.
    -   최초 로딩 시점에 서블릿 객체를 미리 만들어두고 재활용 합니다.
    -   모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근합니다.
    -   따라서 공유 변수 사용에 주의해야 합니다.
-   서블릿 컨테이너 종료시 함께 종료됩니다.
-   JSP도 서블릿으로 변환 되어서 사용됩니다.
-   동시 요청을 위한 멀티 쓰레드 처리를 지원합니다.

---

# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)
- [Learn Servlet Tutorial - javatpoint](https://www.javatpoint.com/servlet-tutorial)