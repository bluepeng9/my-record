- 작성일: 2023-05-05
- 태그: 
- 분류
    - [JAVA](JAVA.md)
- 관련 노트
    - [Web Server와 Web Application Server](../Spring/Web%20Server와%20Web%20Application%20Server.md)
    - [HTTP 메서드 종류](../HTTP/HTTP%20메서드%20종류.md)
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

# 사용 예

## request.getParameter

```java
//http://localhost:8080/servlet/members/save?username=kim&age=20
@WebServlet(
    name = "memberSaveServlet",
    urlPatterns = "/servlet/members/save"
)  
public class MemberSaveServlet extends HttpServlet {
    @Override  
    protected void service(
        HttpServletRequest request,
        HttpServletResponse response
    ) throws ServletException, IOException {  
        String username = request.getParameter("username");  
        int age = Integer.parseInt(request.getParameter("age"));
    
        response.setContentType("text/html");  
        response.setCharacterEncoding("utf-8");
        
        PrintWriter w = response.getWriter();  
        w.write("<html>\n");
        ...
}
```

`request.getParameter`를 통해 `/servlet/members/save` 주소로 온 `request`의 `parameter`를 얻을 수 있습니다.

`POST` 요청 역시 `getParameter`를 이용해 받을 수 있습니다. 
```java
w.write("<!DOCTYPE html>\n" +  
        "<html>\n" +  
        "<head>\n" +  
            " <meta charset=\"UTF-8\">\n" +  
            " <title>Title</title>\n" +  
        "</head>\n" +  
        "<body>\n" +  
        "<form action=\"/servlet/members/save\" method=\"post\">\n" +  
            " username: <input type=\"text\" name=\"username\" />\n" +  
            " age: <input type=\"text\" name=\"age\" />\n" +  
            " <button type=\"submit\">전송</button>\n" +  
        "</form>\n" +  
        "</body>\n" +  
        "</html>\n");
```

위와 같이 `form`을 갖고 있는 `html`에서 `POST` 요청을 보낼 경우 메시지 body 값이 `username=kim&age=20`이 됩니다.

## request.getInputStream

```java
@Override  
protected void service(
    HttpServletRequest request,
    HttpServletResponse response
) throws ServletException, IOException {
    ServletInputStream inputStream = request.getInputStream();  
    
    String messageBody = StreamUtils.copyToString(
        inputStream,
        StandardCharsets.UTF_8
    );  
      
    System.out.println("inputStream = " + inputStream);  
    System.out.println(messageBody);
    ...
}
```

`inputStream`을 활용하여 `messageBody`를 읽어올 수 있습니다.

```java
private final ObjectMapper objectMapper = new ObjectMapper();

...

HelloData helloData = objectMapper.readValue(
    messageBody,
    HelloData.class
);
```

`json` 데이터를 받아 Mapping 시키는 예 입니다.

## request.getRequestDispatcher

```java
@WebServlet(name = "mvcMemberFormServlet", urlPatterns = "/servlet/mcv/members/new-form")  
public class MvcMemberFormServlet extends HttpServlet {  
    @Override  
    protected void service(
        HttpServletRequest request,
        HttpServletResponse response
    ) throws ServletException, IOException {  
        String viewPath = "/WEB-INF/views/new-form.jsp";  

        RequestDispatcher dispatcher = request.getRequestDispatcher(viewPath);  

        dispatcher.forward(request, response);  
    }  
}
```

`dispatcher.foward`를 사용하면 리다이렉트를 사용하지 않고 클라이언트가 방문할 웹 페이지를 정합니다.

## request.setAttribute

```java
request.setAttribute("members", members);
```

`attribute`의 이름, 값을 설정합니다. `html/jsp` 파일로 전달할 수 있습니다.



---
# Reference

- [스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1)
- [Learn Servlet Tutorial - javatpoint](https://www.javatpoint.com/servlet-tutorial)