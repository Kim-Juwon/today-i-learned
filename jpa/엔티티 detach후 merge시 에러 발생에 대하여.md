# 엔티티 detach후 merge시 에러 발생에 대하여
## 상황
비영속 엔티티를 persist()로 영속화한 후 detach()로 준영속화하고, 다시 merge()로 영속화하였을때 Exception 발생
### 코드 
EntityManagerFactory, EntityManager, EntityTransaction까지 모두 이상 없는 상태.

```java
...

transaction.begin();

Member member = new Member();
member.setId("1");
member.setUsername("김주원");
member.setAge(23);

// member 영속화
entityManager.persist(member);
// member 준영속화
entityManager.detach(member);

// member 영속화
member = entityManager.merge(member);

transaction.commit();

...
```
### 에러 로그
```
11:40:15.415 [main] ERROR org.hibernate.AssertionFailure - HHH000099: an assertion failure occurred (this may indicate a bug in Hibernate, but is more likely due to unsafe use of the session): org.hibernate.AssertionFailure: possible non-threadsafe access to session
```

### 원인
에러 로그에 나와있는대로 하이버네이트 내부 버그일 가능성이 높다.
`this may indicate a bug in Hibernate, but is more likely due to unsafe use of the session`

실무에서 jpa사용시 개발자가 직접 detach()를 호출하는 경우는 거의 없을 뿐더러, detach() 호출 후 merge()를 또 호출하는 일은 없기 때문에 크게 고민할 이유가 없다고 함.

참고로 persist()와 detach() 사이에서 flush()를 호출할 경우에는 에러가 발생하지 않는다.

```
entityManager.persist(member);
entityManager.flush();
entityManager.detach(member);
member = entityManager.merge(member);
```

아마도 하이버네이트 내부 프로세스 이벤트와 관련된 버그로 추정.

### 레퍼런스
[https://www.inflearn.com/questions/304787](https://www.inflearn.com/questions/304787)