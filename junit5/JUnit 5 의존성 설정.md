# JUnit 5 의존성 설정
JUnit 5 라이브러리를 사용하기 위한 의존성 설정에 대해 알아본다.

### Spring Boot 2.2 이상 버전

- 스프링부트 2.2 버전 이상 버전부터는 빌드 설정 파일에 별다른 의존성 설정을 하지 않아도 된다.
	- spring-boot-starter에서 제공해주기 때문이다. 
	
<img src="./라이브러리 의존성.png" width="60%">
	
### Spring Boot 2.1 이전 버전

- 스프링부트 2.1 이전 버전은 spring-boot-starter에서 JUnit4.x 버전을 제공한다.

### 그 외

- 자동 의존성이 설정되어있지 않은 프로젝트에서는 직접 설정해주면 된다.
	- [https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-engine](https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-engine) 
