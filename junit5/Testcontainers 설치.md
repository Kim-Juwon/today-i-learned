# Testcontainers 설치
Testcontainers를 사용하기 위한 세팅 방법에 대해 알아본다.

## 모듈
### Testcontainers JUnit5 지원 모듈
- [https://www.testcontainers.org/test_framework_integration/junit_5/](https://www.testcontainers.org/test_framework_integration/junit_5/)
 
```xml
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>1.17.3</version>
    <scope>test</scope>
</dependency>
```

#### @TestContainers와 @Container
- @TestContainers
	- 테스트 클래스에 @Container를 선언하는 필드를 찾아서 컨테이너의 라이프사이클(시작과 종료) 관련 메소드를 실행해준다.
	- org.testcontainers.junit.jupiter에 정의되어 있다.
	- JUnit 5 확장팩이다.
- @Container
	- 인스턴스 필드에 사용할 시: 모든 테스트 메소드마다 컨테이너 재시작
	- static 필드에 사용할 시: 클래스 내부 모든 테스트 메소드에서 동일한 컨테이너 재사용
	- org.testcontainers.junit.jupiter에 정의되어 있다.

### 컨테이너 실행을 위한 여러 모듈
- 각 모듈은 별도로 설치해야 한다.
	- [https://www.testcontainers.org/modules/databases/](https://www.testcontainers.org/modules/databases/)
 
```xml
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>mysql</artifactId>
    <version>1.17.3</version>
    <scope>test</scope>
</dependency>
```

## 코드

```java
import org.junit.jupiter.api.Test;
import org.testcontainers.containers.MySQLContainer;
import org.testcontainers.junit.jupiter.*;

@Testcontainers
class MyTest {
    @Container
    static MySQLContainer mySQLContainer = new MySQLContainer("mysql");

    @Test
    void test() {
        System.out.println("aaa");
    }
}
```