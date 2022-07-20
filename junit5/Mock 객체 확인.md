# Mock 객체 확인
Mock 객체가 어떻게 사용되었는지 확인하는 방법의 대표적인 예시를 알아본다.

### 특정 메소드가 특정 파라미터로 몇번 호출 되었는지 확인
verify() 메소드를 사용하며, 인자에 times(호출 횟수) 메소드가 들어간다. (전부 org.mockito.Mockito에 정의되어 있는 메소드이다.) 

- Mock 객체의 특정 메소드가 특정 파라미터로 호출 횟수만큼 호출되었으면 통과한다.

```java
import com.kimjuwon.junit5study.service.UserService;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock UserService userService) {
        userService.displayUserById(1l);

        // userService Mock 객체의 displayUserById()에 인자를 1로 넣어 1번 호출되었는지 확인
        verify(userService, times(1)).displayUserById(1l); // 통과
    }
}
``` 

- 0번 호출되었는지 확인하고 싶다면 호출 횟수 인자를 0으로 하거나, 그 대신 never() 메소드를 사용할 수도 있다.

```java
import com.kimjuwon.junit5study.service.UserService;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock UserService userService) {
        verify(userService, never()).displayUserById(1l); // 한번도 호출되지 않았으므로 통과
    }
}
```

- verify()에서 Mock 객체의 메소드 인자로 ArgumentMatchers의 메소드를 넣는 것 역시 가능하다.

```
import com.kimjuwon.junit5study.service.UserService;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock UserService userService) {
        verify(userService, never()).displayUserById(any());
    }
}
```

- 그 외는 [공식문서](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#exact_verification) 참조

### 특정 메소드가 특정 순서로 호출되었는지 확인
-  org.mockito.Mockito 클래스의 inOrder() 메소드로 org.mockito.InOrder 타입의 객체를 받은 다음 verify()를 호출하여, 호출한 순서대로 실제 메소드가 호출되었는지 확인한다.

```java
import com.kimjuwon.junit5study.service.UserService;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InOrder;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock UserService userService) {
        User user = userService.findUserById(1l);
        userService.displayUserById(1l);

        InOrder inOrder = inOrder(userService);
        
        // 통과
        inOrder.verify(userService).findUserById(1l); 
        inOrder.verify(userService).displayUserById(1l);
    }
}
```

- 그 외는 [공식문서](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html#in_order_verification) 참조

## 특정 시점 이후에 아무 일도 벌어지지 않았는지
verifyNoMoreInteraction