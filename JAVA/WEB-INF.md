- 작성일: 2023-05-07
- 태그: 
- 분류
    - [JAVA](JAVA.md)
- 관련 노트
---

>A special directory exists within the application hierarchy named `WEB-INF`. This directory contains all things related to the application that aren’t in the document root of the application. **The `WEB-INF` node is not part of the public document tree of the application**. No file contained in the `WEB-INF` directory may be served directly to a client by the container. However, the contents of the `WEB-INF` directory are visible to servlet code using the `getResource` and `getResourceAsStream` method calls on the `ServletContext`, and may be exposed using the `RequestDispatcher` calls.

애플리케이션에 존재하는 특별한 디렉토리입니다. 애플리케이션에 속하지만 document 루트에는 없는 것들을 포함합니다. `WEB-INF` 노드는 애플리케이션의 public 문서 트리에 속하지 않습니다. 

따라서 `WEB-INF`에 속한 모든 파일은 Client가 직접 접근 할 수 없습니다. 대신 servlet을 통한 접근은 가능합니다.

---

# Reference

- [servlets - What is WEB-INF used for in a Java EE web application? - Stack Overflow](https://stackoverflow.com/questions/19786142/what-is-web-inf-used-for-in-a-java-ee-web-application)