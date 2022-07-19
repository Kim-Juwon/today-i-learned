# Mockito 시작하기
Mockito를 사용하기 위해 필요한 라이브러리 세팅에 대해 알아본다.

## 라이브러리
- mockito-core와 mockito-junit-jupiter를 추가해주어야 한다.
	- mockito-core
		- Mockito의 기능 제공
	- mockito-junit-jupiter
		- JUnit을 Mockito와 연동해주는 Extension 구현체

### 프로젝트에 따른 설정
- Spring Boot 프로젝트라면 spring-boot-starter-test에서 mockito-core와 mockito-junit-jupiter를 제공한다.
- 그 외 프로젝트라면 빌드 툴 설정 파일에 의존성을 추가해주어야 한다.
	- mocktio-core: [https://mvnrepository.com/artifact/org.mockito/mockito-core](https://mvnrepository.com/artifact/org.mockito/mockito-core)
	- mocktio-junit-jupiter: [https://mvnrepository.com/artifact/org.mockito/mockito-junit-jupiter](https://mvnrepository.com/artifact/org.mockito/mockito-junit-jupiter)

