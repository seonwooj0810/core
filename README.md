# 스프링 핵심 원리 - 기본편

인프런 김영한 강의 **[스프링 핵심 원리 - 기본편](https://www.inflearn.com/course/스프링-핵심-원리-기본편)** 을 따라하며 학습한 코드입니다.
순수 자바 코드로 작성한 예제(`AppConfig`)를 점진적으로 스프링 컨테이너로 옮기면서 DI(의존관계 주입), IoC, 싱글톤, 컴포넌트 스캔 등 스프링의 핵심 원리를 다룹니다.

## 사용 기술

- Java 11
- Spring Boot 2.7.4 (`spring-boot-starter`, `spring-boot-starter-web`)
- `javax.inject` (JSR-330)
- Lombok
- JUnit 5 (`spring-boot-starter-test`)
- Gradle

## 학습한 내용

코드와 테스트로 확인되는 주제입니다.

### 객체 지향 설계와 스프링
- 회원/주문/할인 도메인 예제 (`member`, `order`, `discount` 패키지)
- 할인 정책을 인터페이스(`DiscountPolicy`)와 구현체(`FixDiscountPolicy`, `RateDiscountPolicy`)로 분리하여 OCP/DIP 적용
- `AppConfig`를 통한 수동 의존관계 주입 / `appConfig.xml` 기반 XML 설정 (`xml/XmlAppContext`)

### 스프링 컨테이너와 빈
- 스프링 컨테이너 생성과 빈 조회 (`beanfind` 패키지: 기본 조회, 상속 관계 조회, 동일 타입 조회, 빈 정보 출력)
- `BeanDefinition` 메타 정보 (`beandefinition/beanDefinitionTest`)

### 싱글톤
- 싱글톤 패턴과 싱글톤 컨테이너 (`singleton` 패키지: `SingletonService`, `StatefulService` 상태 공유 문제)
- `@Configuration`과 바이트코드 조작을 통한 싱글톤 보장 (`ConfigurationSingletonTest`)

### 컴포넌트 스캔과 자동 의존관계 주입
- `@ComponentScan` 기반 자동 빈 등록 (`AutoAppConfig`, `scan/AutoAppConfigTest`)
- 컴포넌트 스캔 필터 (`scan/filter`: include/exclude, 커스텀 애노테이션)
- 다양한 의존관계 주입 방법 및 옵션 처리 (`autowired/AutowiredTest`)
- 조회 빈이 여러 개일 때: List/Map 주입(`autowired/AllBeanTest`), `@Qualifier`/`@Primary`, 직접 만든 애노테이션(`annotation/MainDiscountPolicy`)

### 빈 생명주기 콜백
- `@PostConstruct`/`@PreDestroy`, `InitializingBean`/`DisposableBean`, `@Bean(initMethod, destroyMethod)` (`lifecycle/BeanLifeCycleTest`, `NetworkClient`)

### 빈 스코프
- 싱글톤/프로토타입 스코프와 함께 사용 시 문제 (`scope/PrototypeTest`, `SingletonWithPrototypeTest1`)
- 웹 스코프(request scope)와 프록시 (`common/MyLogger`, `web/LogDemoController`, `web/LogDemoService`)

## 프로젝트 구조

```
src/main/java/hello/core
├── AppConfig.java / AutoAppConfig.java   # 수동/자동 설정
├── MemberApp.java / OrderApp.java        # 실행 예제
├── annotation/                           # 커스텀 애노테이션
├── common/MyLogger.java                  # 웹 스코프 예제
├── discount/                             # 할인 정책 (전략 패턴)
├── member/                               # 회원 도메인
├── order/                                # 주문 도메인
└── web/                                  # 웹 스코프 컨트롤러/서비스
src/test/java/hello/core                  # 주제별 학습 테스트
```
