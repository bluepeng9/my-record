- 작성일: 2023-05-07
- 태그: #작성중 
- 분류
    - [Spring](Spring.md)
- 관련 노트
---

`Handler Mapping Component`는 요청을 받으면, 요청을 처리하는 `Handler`를 찾습니다. `Handler는` 일반적으로 `Controller`의 메서드이므로, `Controller`를 찾게 됩니다.
  
비유하자면 다음과 같습니다.

1. 호텔에 손님(`request`)이 방문합니다.
2. 직원(`Handler Mapping Component`)이 손님을 맞이합니다.
3. 직원은 사용가능한 방(`Handler`)을 찾고 손님을 안내합니다.

`HandlerMapping`은 스프링에서 `interface`로 정의됩니다. 이 인터페이스는 다음과 같은`getHandler`  메서드를 갖고 있습니다.

```java
@Nullable  
HandlerExecutionChain getHandler(
    HttpServletRequest request
) throws Exception;
```


---

# Handler mapping 구조


```
HandlerMapping
|
+-- AbstractHandlerMapping
    |
    +-- AbstractHandlerMethodMapping
    |   |
    |   +-- RequestMappingInfoHandlerMapping
    |   |   |
    |   |   +-- RequestMappingHandlerMapping
    |   |   +-- AbstractControllerUrlHandlerMapping
    |   |
    |   +-- AbstractDetectingUrlHandlerMapping
    |       |
    |       +-- ControllerClassNameHandlerMapping
    |       +-- ControllerBeanNameHandlerMapping
    |
    +-- AbstractUrlHandlerMapping
        |
        +-- SimpleUrlHandlerMapping
        +-- BeanNameUrlHandlerMapping
        +-- WebMvcConfigurationSupport$EmptyHandlerMapping
```

위에서 볼 수 있듯이, `HandlerMapping` 컴포넌트는 두 가지로 분류됩니다.

- `AbstractHandlerMethodMapping`
- `AbstractUrlHandlerMapping`

두 `abstract` 클래스 모두 `AbstractHandlerMapping`를 상속받습니다.

---

# AbstractHandlerMapping 클래스

## getHandler 메서드

```
HandlerMapping
|
+-- AbstractHandlerMapping
    |
...
```

`AbstractHandlerMapping`은 `HandlerMapping` 인터페이스를 `implements`하는 `abstract` 클래스 입니다. `AbstractHandlerMapping`은 템플릿 패턴을 사용해서 자식 클래스들이 적절하게 `override` 할 수 있도록 합니다.

`AbstractHandlerMapping`은 를 다음과 같은 작업을 수행하는 `getHandler` 메서드를 갖고 있습니다.

1. 요청에 맞는 `Handler`가 있는지 체크합니다.
2. 만약 있다면 `Handler`를 return 합니다.
3. 없다면 `null`을 return 합니다.

1번 과정은 `getHandlerInternal`이라는 `abstract method`로 되어있기 때문에, 반드시 `Sub class`에서 구현해야 합니다. 나머지 2, 3번은 구현되어 있습니다.

## initApplicationContext 메서드

`AbstractHandlerMapping` 은 `WebApplicationObjectSupport`라는 클래스를 상속 받고 `initApplicationContext` 메서드를 `override` 합니다.

```java
/**  
* Initializes the interceptors.  
* @see #extendInterceptors(java.util.List)  
* @see #initInterceptors()  
*/  
@Override  
protected void initApplicationContext() throws BeansException {  
    extendInterceptors(this.interceptors);  
    detectMappedInterceptors(this.adaptedInterceptors);  
    initInterceptors();  
}
```

### extendInterceptors 메서드

```java
protected void extendInterceptors(List<Object> interceptors) {}
```

`template method`로, `sub class`가 `this.interceptors`에 속해있는 `interceptor`들을 수정할 수 있도록 합니다.

### detectMappedInterceptors 메서드

```java
protected void detectMappedInterceptors(
    List<HandlerInterceptor> mappedInterceptors
) {  
    mappedInterceptors.addAll(
        BeanFactoryUtils.beansOfTypeIncludingAncestors(  
            obtainApplicationContext(),
            MappedInterceptor.class, true, false
    ).values());  
}
```

`Spring MVC`에 존재하는 `MappedInterceptor` 타입의 모든 `bean`을 `this.addedInterceptors`에 추가합니다.

### initInterceptors 메서드

```java
protected void initInterceptors() {  
    if (!this.interceptors.isEmpty()) {  
        for (int i = 0; i < this.interceptors.size(); i++) {  
            Object interceptor = this.interceptors.get(i);  

            if (interceptor == null) {  
                throw new IllegalArgumentException("Entry number " + i + " in interceptors array is null");  
            }  

            this.adaptedInterceptors.add(adaptInterceptor(interceptor));  
        }  
    }  
}
```

`initInterceptors`는 모든 `interceptors`를 초기화 하는 method로 모든 `this.interceptors`의 인터셉터를 `this.adoptedInterceptors`에 추가합니다.

## AbstractHandlerMethodMapping 시리즈

```
HandlerMapping
|
+-- AbstractHandlerMapping
    |  +----------------------------+
    +--|AbstractHandlerMethodMapping|
       +----------------------------+
```

### AbstractHandlerMethodMapping

`AbstractHandlerMethodMapping`은 `AbstractHandlerMapping`을 상속받으며, `InitializingBean` 인터페이스를 구현합니다.

스프링에서는, `InitializingBean`를 구현한 객체를 초기화할 때, `afterPropertiesSet` 메서드를 호출합니다.

`AbstractHandlerMethodMapping` 클래스는 `afterPropertiesSet` 메서드에서 `request`를 `Handler`와 매칭하는 작업을 수행합니다.

`afterPropertiesSet`를 오버라이드한 코드는 다음과 같습니다.

```java
/**
    * Detects handler methods at initialization.
    * @see #initHandlerMethods
*/
@Override
public void afterPropertiesSet() {
    initHandlerMethods();
}
```

`initHandlerMethods` 메서드가 호출되는 것을 알 수 있습니다. `initHandlerMethods`를 살펴보면 어떻게 초기화 작업이 이루어지는지 알 수 있습니다.

```java
/**
    * Scan beans in the ApplicationContext, detect and register handler methods.
    * @see #getCandidateBeanNames()
    * @see #processCandidateBean
    * @see #handlerMethodsInitialized
*/
protected void initHandlerMethods() {
    for (String beanName : getCandidateBeanNames()) {
        if (!beanName.startsWith(SCOPED_TARGET_NAME_PREFIX)) {
            processCandidateBean(beanName);
        }
    }
    handlerMethodsInitialized(getHandlerMethods());
}
```

`getCandidateBeanNames`  메서드는 스프링 컨테이너에 존재하는 모든 `Bean`의 이름을 갖고 옵니다. 이 이름들은 반복문 속 `processCandidateBean(beanName)` 메서드에게 전달됩니다.

`processCandidateBean(beanName)` 메서드는 세 가지 작업을 수행 합니다.

- `Bean`의 이름으로 해당 빈에 해당하는 타입을 찾습니다.
- `isHandler` 메서드로 `bean`을 걸러냅니다. `ishandler` 메서드는 템플릿 메서드로, `RequestMappingHandlerMapping` 의 자식 클래스가 구현합니다. `ishandler` 메서드는 `@Contorller` , `@RequestMapping` 어노테이션이 붙은 빈만 선택합니다.
- `request`와 핸들러 간의 매핑은 `detectHandlerMethods` 메서드에 의해 설정됩니다.

`detectHandlerMethods` 메서드는 두 가지 작업을 합니다.

- `Handler` 내의 `@requestMaping` 어노테이션이 붙은 메서드를 찾습니다.
    - 찾기 위해 `getMappingForMethod`  메서드를 사용합니다.
    - `AbstractHandlerMethodMapping`와 `getMappingForMethod` 는 단순 `abstract` 메서드이며, `RequestMappingHandlerMapping`의 자식 클래스가 구현해 비지니스 로직을 수행합니다.
- `registerHandlerMethod`를 사용해서 메서드를 등록합니다.
    - 등록이란, 발견한 `HandlerMethod`를 `Map`에 가져오는 것을 의미합니다.
    - 만약 이미 같은 `HandlerMethod`가 등록되어 있다면, 예외가 발생합니다.


```
HandlerMapping
|
+-- AbstractHandlerMapping
    |  +----------------------------+
    +--|AbstractHandlerMethodMapping|
       +----------------------------+
```

`AbstractHandlerMapping`의 `getHandlerInternal`는 `AbstractHandlerMethodMapping` 클래스에서 구현됩니다. 

```java
/**
    * Look up a handler method for the given request.
*/
@Override
@Nullable
protected HandlerMethod getHandlerInternal(
    HttpServletRequest request
) throws Exception {
    String lookupPath = initLookupPath(request);
    this.mappingRegistry.acquireReadLock();
    
    try {
        HandlerMethod handlerMethod = lookupHandlerMethod(lookupPath, request);
        
        return (handlerMethod != null ? handlerMethod.createWithResolvedBean() : null);
        
    }
    finally {
        this.mappingRegistry.releaseReadLock();
    }
}
```

`getHandlerInternal` 메서드에서 세 가지 작업이 수행됩니다.

-  `initLookupPath` 메서드에서, `request`는 `url`로 변환됩니다.
-  그러고 나면 적합한 `Handler`를 찾기 위해 `lookupHandlerMethod` 메서드를 사용합니다.
    - `request`와 `lookupPath`를 사용합니다.
- `HandlerMethod`를 찾을 때, `HandlerMethod` 의 `createWithResolvedBean` 메서드가 호출됩니다.
    - `createWithResolvedBean` 메서드는 `HandlerMethod` 객체가 맞는지 체크합니다.
        - `Bean`의 이름을 통해 찾습니다. 

### RequestMappingInfoHandlerMapping

`RequestMappingInfoHandlerMapping` 클래스는 주로  부모 클래스의 `getMatchingMapping` 메서드를 오버라이드 합니다.

`getMatchingMapping` 메서드는 현재 요청에 기반한 `RequestCondition` 에 일치하는 `RequestMappingInfo` 객체를 return 합니다. 

`SpringMVC` 는 `RequestMappingInfo` 객체에 따라 적합한 `Handler`를 가져옵니다.

### RequestMappingHandlerMapping

`AbstractHandlerMethodMapping` 시리즈의 마지막 초기화 단계는 `RequestMappingHandlerMapping` 입니다.

`RequestMappingHandlerMapping` 는 주로 부모 클래스의 3개의 메서드를 오버라이드 합니다.

-  `afterPropertiesSet`
    - 컴포넌트가 초기화 될 때 불리는 메서드 입니다.
        - 컴포넌트의 설정을 저장하는 `BuilderConfiguration` 타입의 객체를 만듭니다.
- `isHandler`
    - `request`를 handle 할 수 있는지 필터링하는 메서드로
        - `@Controller` 와 `@RequestMapping` 어노테이션이 붙은 메서드만 체크합니다.
- `getMappingForMethod`
    - `RequestMappingInfo` 타입의 객체를 만드는데 사용되는 메서드 입니다.
        - 경로, 헤더, 매개변수, MIME 유형, 요청 메서드 등 메서드가 일치시킬 수 있는 요청 조건에 대한 정보가 포함되어 있습니다.
        - `RequestMappingInfo`는 요청이 일치하는지 확인하는 `RequestCondition` 인터페이스를 구현합니다.
            - Spring MVC는 이 인터페이스를 사용해서 가장 일치하는 조건을 찾습니다.



---
# Reference

- [HandlerMapping in Spring MVC - Spring Cloud](https://www.springcloud.io/post/2022-08/spring-mvc-handlermapping/#handlermapping-class-system)