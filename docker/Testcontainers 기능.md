# Testcontainers 기능
Testcontainers의 기능을 살펴본다.

## 컨테이너 만들기
만약 특정 모듈의 testcontainers 라이브러리 클래스가 없다면 이미지를 불러와 만들 수 있다.

- new GenericContainer(String imageName)
	- GenericContainer는 org.testcontainers.containers에 정의되어 있는 클래스
	- GenericContainer 객체 생성 시 인자로 이미지 이름을 넣어주어 컨테이너 생성
		- 해당 이미지가 로컬에 있다면: 컨테이너 실행
		- 해당 이미지가 로컬에 없다면: docker hub(원격 도커 이미지 저장소)에서 가져와서 실행

```java
@Container
static GenericContainer mySQLContainer = new GenericContainer("mysql")
```

### GenericContainer의 다양한 메소드

### 환경 변수 설정
- withEnv(key, value)
	- 컨테이너의 환경 변수를 설정할 수 있다.

```java
@Container
static GenericContainer mySQLContainer = new GenericContainer("mysql")
        .withEnv("MYSQL_ROOT_PASSWORD", "1234");
```

### 네트워크
컨테이너에서 사용할 모듈의 포트를 명시적으로 지정할 수 있다. (host의 포트는 설정할 수 없다. testcontainers에서 랜덤으로 지정.)

- withExposedPorts(int...)
	- 컨테이너에서 사용할 포트를 명시적으로 알려준다.
		- 기본적으로 원래는 이미지에서 default 포트가 있지만 사용자가 직접 명시해 줄 수 있는 것이다.

```java
@Container
static GenericContainer mySQLContainer = new GenericContainer("mysql")
        .withExposedPorts(1234);
```

- getMappedPort(int)
	- 컨테이너의 포트와 매핑된 host의 포트를 얻는다.

### 사용할 준비가 됐는지 확인
- waitingFor(Wait)
	- Wait.forHttp(String path)
		- 특정 uri에 대한 요청이 올때까지 기다렸다가 요청이 오면 테스트 실행
		- Wait: org.testcontainers.containers.wait.strategy.Wait
	- Wait.forLogMessage(String message)
		- 컨테이너에 특정한 로그 메시지가 출력이 됐는지 확인한 다음 테스트 실행
		- Wait: org.testcontainers.containers.wait.strategy.Wait

### 로그 살펴보기
[https://www.testcontainers.org/features/container_logs/](https://www.testcontainers.org/features/container_logs/)

- getLogs()
	- 현재까지 컨테이너 안에 있는 로그를 전부 가져온다.
- followOutput()
	- 로그가 쌓일때마다 애플리케이션에서 출력한다.

### 명령어 실행
- withCommand(String cmd...)
	- 컨테이너의 명령어를 실행할 수 있다.

