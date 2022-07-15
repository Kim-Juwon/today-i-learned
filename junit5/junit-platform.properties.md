# junit-platform.properties
JUnit의 설정 파일인 junit-platform.properties 파일에 대해 알아본다.

## junit-platform.properties
- JUnit의 설정 파일이다.
- classpath root(src/test/resources/)에 넣어두면 적용된다.

### 대표적인 속성
#### junit.jupiter.testinstance.lifecycle.default
테스트 인스턴스 라이프사이클을 설정한다. 
##### value
- `per_method`
	- 테스트 클래스의 메소드별로 인스턴스를 생성한다.
- `per_class`
	- 테스트 클래스별 하나의 인스턴스만 생성한다.

#### junit.jupiter.conditions.deactivate
실행 시 무시할 조건을 설정한다.
##### value
- `org.junit.*DisabledCondition`
	- @Disabled 무시
- `org.junit.*DisabledOnOsCondition`
	- @DisabledOnOs 무시
- `org.junit.*DisabledOnJreCondition`
	- @DisabledOnJre 무시

#### junit.jupiter.displayname.generator.default
테스트 이름 표기 전략을 설정한다.
##### value
- `org.junit.jupiter.api.DisplayNameGenerator$ReplaceUnderscores`
	- replace underscores(언더바를 공백문자로 치환) 표기 전략 적용

#### junit.jupiter.extensions.autodetection.enabled
확장팩 자동 감지 기능을 쓸 것인지에 대한 여부를 설정한다.

자세한 내용은 [공식 문서](https://junit.org/junit5/docs/current/user-guide/#extensions-registration-automatic) 참조
##### value
- `true`: 기능을 사용한다.
- `false`: 기능을 사용하지 않는다.
