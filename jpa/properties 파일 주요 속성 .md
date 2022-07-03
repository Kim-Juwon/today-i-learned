# properties 파일 주요 속성 
스프링부트에서 JPA(Hibernate) 관련 설정파일 작성시 주요 속성의 종류와 뜻에 대해 알아본다.

```yml:properties.yml
spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/test 
    username: sa 
    password: 
    driver-class-name: org.h2.Driver

  jpa:
    hibernate:
      ddl-auto: create 
    properties:
      hibernate:
#      show_sql: true 
        format_sql: true 

logging:
  level:
    org.hibernate.SQL: debug # hibernate를 통해 CRUD를 실행하면 해당 CRUD의 sql을 로깅 (logger)
    org.hibernate.type: trace # sql에 바인딩되는 파라미터 값을 보여줌
```

### spring.datasource
- url: 데이터베이스 URL
- username: 데이터베이스 유저 네임
- password: 데이터베이스 유저 비밀번호
- driver-class-name: 데이터베이스 드라이버

### spring.jpa
- hibernate.ddl-auto: create로 설정시, 애플리케이션이 실행되면 Entity 클래스들의 정보를 보고 db에 create sql 적용
- properties.hibernate.show_sql: true로 설정시, hibernate를 통해 CRUD를 실행하면 해당 CRUD에 대한 sql을 로깅 (System.out)
- properties.hibernate.format_sql: true로 설정시, 로깅에 표시되는 sql을 보기 좋게 표시

### logging.level
- org.hibernate.SQL: debug로 설정시, hiberante를 통해 CRUD를 실행하면 해당 CRUD의 sql을 로깅 (logger)
- org.hibernate.type: trace로 설정시, sql에 바인딩되는 파라미터 값을 보여줌

### **spring.jpa.properties.hibernate.show_sql: true** vs *logging.level.org.hibernate.type: trace*
#### spring.jpa.properties.hibernate.show_sql: true
- System.out으로 로깅

#### logging.level.org.hibernate.type: trace
- logger를 통해 로깅

#### 무엇을 사용해야 하는가?
- 일반적으로는 System.out보다 logger가 더 장점이 많기때문에 logger를 쓰는 경우가 많다.
- [참고1](https://www.baeldung.com/java-system-out-println-vs-loggers)
- [참고2](https://blog.silentsoft.org/archives/13)