# Mockito BDD 스타일 API
BDD 스타일을 지원하는 Mockito API를 사용해보자.

## BDD란
- Behavior-Driven Development (행위 주도 개발)
- 애플리케이션이 어떻게 행동해야하는지에 대한 공통된 이해를 구성하는 방법
- TDD에서 파생되었음

### 행동에 대한 스펙
- title: 이름
- Narrative: 설명
	- As a / I want / so that
- Acceptance criteria: 인수 조건
	- Given / When / Then

### BddMockito API
#### when -> given
- when() 메소드 대신 org.mockito.BDDMockito 클래스의 given() 메소드를 사용

```java
// userService Mock 객체의 findUserById()에 인자 1을 넣고 호출하면 user 객체 리턴
given(userService.findUserById(1l)).willReturn(user);
```

#### verify -> then
- verify() 메소드 대신 org.mockito.BDDMockito 클래스의 then() 메소드를 사용

```java
then(userService).should(times(1)).findUserById(1l);
then(userService).shouldHaveNoInteractions();
```

#### 그 외
- 공식 문서 참조
	- [https://javadoc.io/static/org.mockito/mockito-core/3.2.0/org/mockito/BDDMockito.html](https://javadoc.io/static/org.mockito/mockito-core/3.2.0/org/mockito/BDDMockito.html)
	- [https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#BDD_behavior_verification](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#BDD_behavior_verification)