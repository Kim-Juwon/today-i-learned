# Mock 객체 만들기
Mock 객체를 만드는 방법을 알아본다.

## Mock 객체 만드는 방식
메소드로 만드는 방식과 어노테이션으로 만드는 방식이 있다.

### 메소드로 만드는 방식
- org.mockito.Mockito 클래스의 mock() static 메소드를 호출한다.
	- 인자로 타입을 넣어주면 해당 타입의 Mock 객체를 리턴해준다.

```java
import org.junit.jupiter.api.Test;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

class MyTest {
    @Test
    void test() {
        // PlayerService 타입의 mock 객체 생성
        PlayerService playerService = mock(PlayerService.class); 
        
        assertNotNull(playerService); 
    }
}
```

### 어노테이션으로 만드는 방식
- 필드에 선언하는 방식과, 테스트 메소드 파라미터에 선언하는 방식이 있다.
- 두 방식 모두 클래스에 @ExtendWith(MockitoExtension.class)를 선언해야 적용될 수 있다.
	- @ExtendWith: org.junit.jupiter.api.extension.ExtendWith
	- MockitoExtension 클래스: org.mockito.junit.jupiter.MockitoExtension

#### 필드에 선언하는 방식
- 필드에 @Mock(org.mockito에 정의되어 있는 어노테이션)을 선언한다.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Mock
    PlayerService playerService;

    @Test
    void test() {
        assertNotNull(playerService);
    }
}
```

#### 파라미터에 선언하는 방식
- 파라미터에 @Mock(org.mockito에 정의되어 있는 어노테이션)을 선언한다.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock PlayerService playerService) {
        assertNotNull(playerService);
    }
}
```