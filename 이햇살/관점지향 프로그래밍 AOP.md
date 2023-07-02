# 관점지향 프로그래밍 AOP

## 1. AOP (Aspect Oriented Programming)

- 관점 지향 프로그래밍(AOP) 는 `횡단 관심사를 분리`하여 `모듈성을 증가`시키는 것

  - `횡단 관심사(cross-cutting concern)` : 백엔드 애플리케이션이 갖춰야 할 요구사항 중에는 `로깅, 보안, 트랜잭션` 같은 애플리케이션 전반에 걸쳐 제공해야 하는 공통 요소들
  - 소스 코드에서 횡단 관심사를 분리하지 않으면 비즈니스 로직과 횡단 관심사 코드가 섞여 코드가 이해하기 어렵게 되고 모듈로서의 응집도가 떨어짐

- 객체 지향 프로그래밍(OOP)의 단점을 해소하기 위해 등장

  - 모든 변수 선언시 new를 통해 객체를 선언
  - 객체를 재사용 한다는 측면에서 효율적이었으나, 공통된 부가기능에 대한 코드가 중복,반복된다는 단점

- 하나의 소프트웨어가 하나의 거대한 OOP로써 설계, 프로그래밍 되었다면 이것을 각 기능별로 `모듈화 해서 분리`를 시키는 개념

  <img src="C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230702203027474.png" alt="image-20230702203027474" style="zoom: 67%;" />

  - 기존의 단순 OOP에서는 계좌이체, 입출금, 이자계산의 서비스가 각각의 OOP로 프로그래밍 되었고, 각각의 OOP 모두 기능 작동을 위해 로깅, 보안, 트랜잭션을 하는 코드가 구현

  - 그런데 계좌이체, 입출금, 이자계산 비즈니스 모두가 공통적으로 갖는 로직이 존재

  - 그렇다면 이것을 각각의 OOP 소스코드에서 제거하고 외부로 빼내 하나의 공통 모듈 생성

    → 이것이 바로 기존의 OOP에 AOP 관점을 더해 발전시킨 기법

```java
class A {
	method a() {
		AAAA
		method a 가 하는 일
		BBBB
	}

	method a() {
		AAAA
		method b 가 하는 일
		BBBB
	}
}

class B {
	method c() {
		AAAA
		method c 가 하는일
		BBBB
	}
}
```

- AAAA, BBBB는 여러군데에서 중복적으로 사용하는 코드

  - 중복된 코드 → 비효율
  - AAAA, BBBB 수정시 여러 군데에 있는 코드 수정해줘야함 → 비효율

- AOP는 흩어진 관심사를 모아서 모듈화 시킴

  - 여기저기에 흩어져서 반복되는 코드를 흩어진 관심사 → 관심사 관점으로 생각하는게 관점지향 프로그래밍

  - 중복되는 코드를 모듈화 하고 핵심적인 비즈니스 로직에서 분리하여 재사용

    <img src="C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230702210233089.png" alt="image-20230702210233089" style="zoom: 50%;" />

### 2. AOP의 주요 개념, 어노테이션

- Spring
  - `Aspect`
    - 흩어진 관심사를 묶어서 모듈화 한 것. 하나의 모듈
    - Advice와 Point Cut이 들어간다
  - `Advice`
    - 해야할 일들에 대한 정보
  - `JointPoint`
    - Advice 가 적용될 위치, 끼어들 수 있는 지점, 메서드 진입 지점 등 다양한 시점 등 어디에 적용해야하는지에 대한 정보
    - 다른 AOP 프레임워크와 달리 Spring에서는 메소드 조인포인트만 제공
    - 함수가 Before(실행 전), After(실행 후), AfterReturning(반환 후), AfterThrowing(예외 발생시), Around(실행 전과 후)
  - `PointCut`
    - JointPoint의 상세한 스펙을 정의한 것
    - 구체적으로 Advice가 실행될 시점
  - `Target`
    - Advice가 적용되는 대상(클래스, 메서드 등)
    - 부가기능을 부여할 대상
  - `Weaving`
    - Aspect(when + where) + Advice(what)
    - 위빙을 통해 지정된 객체를 새 Proxy 객체로 생성
  - `Proxy`
    - Crosscut Concern(횡단 관심)이 Core Concern(핵심 관심)에서 직접 실행되지 않고 Proxy(대리인)을 생성해 실행
- Spring boot
  - @Aspect : AOP를 정의하는 클래스에 할당
  - @Pointcut : AOP를 적용 시킬 지점 설정
  - @Before : 메소드 실행하기 이전
  - @After : 메소드가 성공적으로 실행 후 예외가 발생되더라도 실행
  - @AfterReturing : 메소드 호출 성공 실행 시
  - @AfterThrowing : 메소드 호출 실패 예외 발생
  - @Around : Before/After 모두 제어

### 3. 스프링 AOP의 특징

- 스프링에서 AOP 구현은 접근 제어 및 부가기능을 추가하기 위해서 Proxy를 이용

  - 프록시 패턴을 이용해 AOP 효과를 냄 (접근 제어 및 부가기능을 추가하기 위해)

  - 이 때문에 다른 AOP의 기능과 비교해서 매우 제한적인 부분만을 지원

- 스프링 내에 프록시 빈에서만 AOP를 적용 가능

  - 설정 구조 상 다른 XML기반의 AOP에 비해 복잡

- 모든 AOP 기능을 제공하는 것이 목적이 아니라, 스프링 IoC와 연동하여 애플리케이션에서 가장 흔히 발생하는 문제(중복코드, 프록시 클래스 작성의 번거로움, 객체 간 관계 복잡도 등)를 해결하기 위한 솔루션을 제공하는것이 목적

#### 3.1 프록시 패턴

<img src="C:\Users\haetsal\AppData\Roaming\Typora\typora-user-images\image-20230702205117169.png" alt="image-20230702205117169" style="zoom:80%;" />

- 특징
  - interface가 존재하고, client는 interface 타입으로 proxy 객체를 사용
  - Real Subject는 Subject라는 interface를 구현한 객체. 원래 해야할 일을 가지고 있다
  - Proxy는 Subject를 구현하면서, 원래해야할 일을 가지고 있는 Real Subject를 의존(의존성 주입)해서 생성된 객체. Client의 요청을 처리
- 사용하는 이유
  - 원래의 Client와 Real Subject의 코드를 건드리지 않고 부가기능을 추가 가능
- Spring AOP는 동적으로 Proxy 생성
  - 정적으로 Proxy를 만들었을 때의 단점
    - Proxy를 만드는데 생기는 비용과 수고가 발생
    - Proxy를 여러 클래스, 메소드에 적용시켜야 한다면 매번 프록시 클래스 작성해야함
  - 런타임, 즉 애플리케이션이 동작하는 중에 proxy 객체 생성함으로써 해결

### 4. AOP개념을 도입함으로써 얻는 장점

- 각 비즈니스 로직마다 복붙을 통해 생겨난 중복 코드 정리
- 각 비즈니스 로직을 구현하는 개발자는 자기 자신의 비즈니스 코드에만 집중할 수 있어 코드가 간결해지고, 유지보수가 쉬워짐
- 재활용성이 더욱 높아짐

### 5. AOP가 필요한 이유

- **애플리케이션의 핵심 로직과 공통 기능을 분리하는 이유**
  - 코드의 간결성 유지
  - 객체 지향 설계 원칙에 맞는 코드 구현
  - 코드의 재사용

---

참고자료

[[Spring] AOP란 무엇인가? (관점 지향 프로그래밍)](https://ittrue.tistory.com/213)

[관점 지향 프로그래밍 (AOP, Aspect-Oriented Programming)](https://assu10.github.io/dev/2023/02/26/aop/)

[OOP (객체지향), AOP(관점지향)](https://greendreamtrre.tistory.com/601)

[AOP(관점 지향 프로그래밍)](https://velog.io/@mdy0102/AOP%EA%B4%80%EC%A0%90-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)