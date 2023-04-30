|       분류       |       내용                                                                                                                                                                                                                                                                                                                                                                                                        |
|:---------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       태그       |     |
|       분류       |                                                                                                                                                                                                                                                                                                                                                                                                  |  

# SOLID 란
---
로버트 마틴이 2000년대 초반에 명명한 객체 지향 프로그래밍 및 설계의 다섯 가지 기본 원칙

# 구성 요소
---

## S : 단일 책임 원칙 (Single responsibility principle)

한 클래스는 하나의 원칙만 가져야 한다는 원칙. 예를 들어 A라는 로직이 존재한다면 어떠한 클래스는 A에 관한 클래스여야 하고 이를 수정한다고 했을 때도 A와 관련된 수정이어야 합니다.

### 위배 예시
```java
pulbic class SuperMarket { 
	private String owner; // 주인
	private String snack; // 과자
	private int snackCount; // 과자 갯수
	
	/* 위배 */ 
	public void fnPay() {} // 결제 public 
	void fnMoneyCharge() {} // 카드 충전
}
```
슈퍼마켓 클래스에서 여러가지 행동을 의미하는 메서드를 사용하여 SRP를 위배 하였음

## O : 개방-폐쇄 원칙 (Open/closed principle)

개방-폐쇄 원칙(OCP, Open Closed Principle)은 유지 보수 사항이 생긴다면 코드를 쉽게 확장할 수 있도록 하고 수정할 때는 닫혀 있어야 하는 원칙입니다. 즉, 기존의 코드는 잘 변경하지 않으면서도 확장은 쉽게 할 수 있어야 합니다.

### 위배 예시
```java
void incAll(Employee[] emps) {
    for (int i=0; i<emps.size(); i++) {
        if(emps[i].empType == FACULTY)
            incFacultySalary((FACULTY)emps[i])
        else if(emps[i].empType == STAFF)
            incStaffSalary((STAFF)emps[i])
        else if(emps[i].empType == SECRETARY)
            incSecretarySalary((SECRETARY)emps[i])
    }
}
```
empType 이 추가될 때 마다 변경이 필요함.

## L : 리스코프 치환 원칙 (Liskov substitution principle)

리스코프 치환 원칙(LSP, Liskov Substitution Principle)은 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 하는 것을 의미합니다. 클래스는 상속이 되기 마련이고 부모, 자식이라는 계층 관계가 만들어집니다. 이때 부모 객체에 자식 객체를 넣어도 시스템이 문제없이 돌아가게 만드는 것을 말합니다. 즉, 범석 객체가 홍철 객체의 자식 계층일 때 범석 객체를 홍철 객체와 바꿔도 문제가 없어야 하는 것을 말합니다

### 위배 예시
#### java 패키지에서의 위배
```java
java.util.Date date = new java.util.Date();
int dateValue = date.getDate(); // Okay

date = new java.sql.Time(10,10,10);
dataValue = date.getDate(); // throws IllegalArgumentException
```
java.sql.Time 은 java.util.Date 를 상속하지만 java.util.Date에 있는 메소드 getDate를 사용할 수 없다(Deprecated)

#### 직사각형, 정사각형 문제


## I : 인터페이스 분리 원칙 (Interface segregation principle)

인터페이스 분리 원칙(ISP, Interface Segregation Principle)은 하나의 일반적인 인터페이스보다 구체적인 여러 개의 인터페이스를 만들어야 하는 원칙을 말합니다. ex) 남자, 아들

## D : 의존관계 역전 원칙 (Dependency inversion principle)

의존 역전 원칙(DIP, Dependency Inversion Principle)은 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는 원칙을 말합니다. 예를 들어 타이어를 갈아끼울 수 있는 틀을 만들어 놓은 후 다양한 타이어를 교체할 수 있어야 합니다. 즉, 상위 계층은 하위 계층의 변화에 대한 구현으로부터 독립해야 합니다.

### 적절하게 사용할 수 있는 상황 (맞는 지 확인 X)
![Pasted image 20230408141951](%EC%B2%A8%EB%B6%80%20%ED%8C%8C%EC%9D%BC/Pasted%20image%2020230408141951.png)
![Pasted image 20230408142001](%EC%B2%A8%EB%B6%80%20%ED%8C%8C%EC%9D%BC/Pasted%20image%2020230408142001.png)
순환 의존성이 생겼을 때.
usecase 의 input 을 받을 때?


# 출처
---
[21. SOLID (객체 지향 설계) - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/SOLID_(%EA%B0%9D%EC%B2%B4_%EC%A7%80%ED%96%A5_%EC%84%A4%EA%B3%84))
[20. 면접을 위한 CS 전공지식 노트: 1.2.2 객체지향 프로그래밍 - 4 (thebook.io)](https://thebook.io/080326/0050/)
[22. [JAVA] SOLID - 단일 책임 원칙 SRP(Single Responsibility Principle) (tistory.com)](https://jeongkyun-it.tistory.com/103)