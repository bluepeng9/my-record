|             |                     |
|:------------|:--------------------|
| 작성일         | 2023-04-08 |
|   분류        |     [[Spring]]                |

# POJO (Plain Old java Obejct)
- 프레임워크 없이도 돌아가는 순수한 자바 객체
- 특정 기술에 종속되지 않는 순수한 자바 객체

# AOP (Aspect Oriented Programming) 관점 지향 프로그래밍
- 트랜잭션이나 로깅, 보안과 같이 여러 모듈에서 공통적으로 사용하는 기능의 경우 해당 기능을 분리하여 사용 가능

# IOC (Inversion of Control) 제어의 역전 / 역행
- 컨트롤의 제어권이 사용자가 아니라 프레임워크에 있어서 필요에 따라 스프링에서 사용자의 코드를 호출한다.

# DI (Dependency Injection) 의존성 주입 / 종속성 주입
- 각각의 계층이나 서비스들 간에 의존성이 존재할 경우 프레임워크가 서로 연결시켜준다.

# PSA (Portable Service Abstraction) 일관성 있는 추상화
- 스프링에서 Controller, Mapping, Trasanction 이런 Annotation(어노테이션)등을 클래스나 메서드에 붙이기만 해주면 작동한다. 이를 가능케 해주는게 바로 PSA 개념이다.  추상화 계층을 사용하여 어떤 기술을 내부에 숨기고 개발자에게 편의성을 제공하는 것을 말한다

## PSA 예시
### Spring Web MVC
클래스에 @Controller 어노테이션을 사용하면 메서드들의 Mapping 정보를 읽을 수 있게 만들어 준다. 이를 구동하게 해주는 것이 내장된 Tomcat이라고 가정해보자. 이때 개발자가 전혀 다른 기술 스택인 WebFlux라는 기술로 이를 구동할 시 개발자가 직접 접근하여 구현할 필요 없이 Spring Web MVC의 추상화 계층을 사용하여 Netty라는 WAS로 구동을 할 수 있다

### JDBC
우리가 DB에 접근할때 JDBC라는 것을 사용하면 Oracle 또는 MySQL 둘 중 아무거나 사용하더라도 접근을 할 수 있다
이 처럼 같은 일을 하는 다수의 기술(Tomcat or Netty 또는 Oracle or MySQL)을 공통의 인터페이스로 제어할 수 있게 한 것을 서비스 추상화라고 한다

# 관련 링크
---

# 출처
---
[19. \[Spring\] Spring Framework란? (velog.io)](https://velog.io/@matcha_/Spring-Spring-Framework%EB%9E%80)
[18. \[Spring\] PSA(Portable Service Abstraction) (tistory.com)](https://maenco.tistory.com/entry/PSAPortable-Service-Abstraction)