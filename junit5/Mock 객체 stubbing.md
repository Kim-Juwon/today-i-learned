# Mock 객체 stubbing
Mock 객체를 stubbing 하는 방법에 대해 알아본다.

## stubbing이란
- Mock 객체를 stubbing 한다는 것은 해당 Mock 객체의 행동을 조작하는 것을 말한다.

## Mock 객체 등록 후 상태
- 필드는 모두 기본값이며, 메소드는 아무일도 수행하지 않는 상태이다.
	- 필드
		- primitive type, primitive wrapper type: 해당 타입의 기본값 
		- reference type: null 
		- collection: 비어있음 (null)
	- 메소드
		- 리턴 타입이 있는 경우 리턴 값
			- primitive type, primitive wrapper type: 기본값 리턴
			- reference type: null 리턴
			- collection: null 리턴
			- Optional type: Optional.empty 리턴
		- 리턴 타입이 없는 경우(void)
			- 예외를 던지지 않고, 아무런 일도 일어나지 않음
- 만약 필드에 기본 값 외 다른 값을 할당한다거나, 메소드에 로직을 추가해도 상태는 계속 그대로다.

## Mock 객체 stubbing 종류
- 위에서 말한 것과 같이 아무것도 아닌 상태의 Mock 객체를 stubbing 하게되면, 해당 Mock 객체의 행동을 조작할 수 있다.
	
### 예시
#### 상황
- UserService 라는 interface가 있다.
	- findUserById(Long userId) 라는 메소드가 있다.
		- User 객체를 리턴한다.

```java
public interface UserService {
    User findUserById(Long userId);
}
```

- UserService 타입에 대한 Mock 객체를 등록하였다.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class)
class MyTest {
    @Test
    void test(@Mock UserService userService) {

    }
}
```

- 현재 UserService Mock 객체는 findUserById() 메소드를 호출해도 아무일도 일어나지 않는다.
	
	 
#### 특정 파라미터를 받은 경우 특정한 값을 리턴
- org.mockito.Mockito의 when().thenReturn() 메소드 사용

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
        User user = new User();
        user.setId(1l);
        user.setName("김주원");

        // 등록한 Mock 객체의 findUserById()에 1을 넣고 호출할경우, user 객체 리턴
        when(userService.findUserById(1l)).thenReturn(user);

        User newUser = userService.findUserById(1l);
        System.out.println(newUser.toString()); // User(id=1, name=김주원)
    }
}
```

#### 불특정 다수 파라미터를 받은 경우 특정한 값을 리턴
- 호출하는 Mock 객체의 인자에 any() 메소드 사용
- 