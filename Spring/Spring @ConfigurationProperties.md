- 작성일: 2023-05-14
- 태그: 
- 분류
    - [Spring](Spring.md)
- 관련 노트

---

```java
@ConfigurationProperties(prefix = "myapp.mail")
class MailModuleProperties {

  private Boolean enabled = Boolean.TRUE;
  private String defaultSubject;

  // getters / setters
  
}
```

스프링에서 메일을 보내는 모듈을 만든다고 상상해 보세요. 로컬 테스트에서는 모듈이 실제로 이메일을 보내지 않도록 하고 싶습니다. 그래서 이 기능을 비활성화할 수 있는 파라미터가 필요합니다.

또한, 메일들의 기본 제목을 설정할 수 있도록 하고 싶습니다. 그러면 우리는 메일함에서 테스트 환경에서 보낸 이메일들을 빠르게 구분할 수 있습니다.

스프링 부트는 이와 같은 파라미터를 애플리케이션에 전달할 수 있는 다양한 옵션을 제공합니다. 다음과 같이 `application.properties`을 만들어 파라미터를 전달할 수도 있습니다.

```properties
myapp.mail.enabled=true
myapp.mail.default-subject=This is a Test
```

애플리케이션 내에서 이러한 프로퍼티들의 값을 Spring의 `Environment` 빈에 요청하거나 `@Value` 어노테이션을 사용하는 등의 방법으로 접근할 수 있게 되었습니다.

그러나 `@ConfigurationProperties` 어노테이션을 붙인 클래스를 생성함으로써 더 편리하고 안전하게 접근하는 방법이 있습니다.

```java
@ConfigurationProperties(prefix = "myapp.mail")
class MailModuleProperties {

  private Boolean enabled = Boolean.TRUE;
  private String defaultSubject;

  // getters / setters
  
}
```

`@ConfigurationProperties` 는 다음과 같은 특징을 갖고 있습니다.

- `prefix`는 클래스의 필드에 바운딩 될 외부 프로퍼티를 정의 합니다.
- 클래스의 프로퍼티 이름은 반드시 외부 프로퍼티와 일치해야 합니다.
- 필드를 값과 함께 초기화 함으로써 기본 값을 지정할 수 있습니다.
- 클래스의 필드는 반드시 `pulibc setter`를 가지고 있어야 합니다.

하지만 아직 스프링이 `@ConfigurationProperties` 클래스의 존재를 모르기 때문에 사용할 수 없습니다.

---

#  @ConfigurationProperties 활성화 하기

`MailModuleProperties` 클래스의 빈을 만들기 위해 Spring boot에서는 여러 가지 방법을 사용할 수 있습니다.

먼저, `@Component` 어노테이션을 추가하여 `MailModuleProperties`를 컴포넌트 스캔의 대상으로 설정할 수 있습니다.

```java
@Component
@ConfigurationProperties(prefix = "myapp.mail")
class MailModuleProperties {
  // ...  
}
```

`@Configuration` 어노테이션을 사용해도 같은 결과를 얻을 수 있습니다.

```java
@Configuration
class MailModuleConfiguration {

  @Bean
  public MailModuleProperties mailModuleProperties(){
    return new MailModuleProperties();
  }

}
``````

또한 `@EnableConfigurationProperties` 어노테이션을 사용하여 Spring Boot에 클래스를 알릴 수 있습니다:

```java
@Configuration
@EnableConfigurationProperties(MailModuleProperties.class)
class MailModuleConfiguration {

}
```

## 어떤 방법이 최고일까?

위의 방법에서 모두 같은 결과를 얻을 수 있습니다. 하지만 `@EnableConfigurationProperties`를 사용한다면 다른 모듈에 영향을 미칠 수 있습니다.

따라서 필자는 private 접근 제한자를 사용할 수 있는 `@Configuration`을 사용하여 나머지 애플리케이션으로부터 프로퍼티를 숨기는 방법을 선호합니다.


---

# Reference

- [Configuring a Spring Boot Module with @ConfigurationProperties (reflectoring.io)](https://reflectoring.io/spring-boot-configuration-properties/)