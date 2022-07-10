# JUnit 5의 구조
JUnit 5는 JUnit 4와 구조적으로 어떻게 다른지, 특징에 대해 살펴본다.

### JUnit 4와의 구조적 차이점
- JUnit 4
	- 빌드 설정 파일에서 의존성을 설정한 하나의 JUnit 4 라이브러리(jar)가 JUnit 4 관련 상세 라이브러리들에 의존하고 있는 구조
- JUnit 5
	- JUnit 5 자체로 모듈화가 되어있다.
	- Platform 위에 Jupiter와 Vintage를 올릴 수 있는 구조

### 구조
<img src="./JUnit 5 구조.png" width="60%" height="60%">

- JUnit Platform
	- JUnit 테스트를 실행해주는 launcher
	- @Test 어노테이션이 붙은 메소드를 JUnit platform이 실행시켜준다.
		- 자바는 기본적으로 main() 으로만 프로그램을 실행할 수 있다.
	- TestEngine API를 제공한다.
- Jupiter, Vintage
	- TestEngine API의 구현체
	- Jupiter는 JUnit 5를 지원하고, Vintage는 JUnit 3과 4를 지원하다.
		- 따라서 JUnit 5를 사용하고자 한다면 Jupiter만 사용해도 큰 문제가 없다.

