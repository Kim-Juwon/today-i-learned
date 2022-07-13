# @ManyToOne과 @JoinColumn
연관관계 매핑을 위한 @JoinColumn 어노테이션과 @ManyToOne 어노테이션에 대해 알아본다.

## @ManyToOne
다대일(N:1) 관계임을 나타낸다.

#### 속성
`optional`

- false로 설정하면 연관된 엔티티가 항상 있어야 한다.
- 기본값: true

`fetch`

- 연관관계에 있는 객체를 즉시 로딩할것인지 지연로딩할것인지 정한다.
- javax.persistence의 FetchType enum 타입의 값을 이용한다.
	- FetchType.EAGER: 즉시 로딩
	- FetchType.LAZY: 지연 로딩
- 기본값: FetchType.EAGER

`cascade`

- 영속성 전이 기능
- 자새한 내용은 8장에서 설명

`targetEntity`

- 연관관계에 있는 엔티티의 타입을 설정한다.
- 컬렉션을 사용한다고 해도 제네릭으로 타입을 알 수 있기 때문에 거의 사용하지 않는다.

#### 예시

```java
@Entity
@Table(name = "players")
public class Player {
    ...

    @ManyToOne // Player와 Team은 다대일 관계
    private Team team;

    ...    
}
```

#### 참고
@ManyToOne 말고도 @OneToMany(일대다), @OneToOne(일대일) 어노테이션도 있다.

이것은 뒤에서 알아보기로 한다.

## @JoinColumn
객체에서 참조 필드에 외래키를 매핑할 때 사용한다.

#### 속성
`name`

- 매핑할 FK 컬럼명
- 기본값: 필드명 + _ + 참조하는 테이블의 PK 컬럼명

`referencedColumnName`

- 외래 키가 참조하는 대상 테이블의 컬럼명 (PK 컬럼명)
- 기본값: 참조하는 테이블의 PK 컬럼명

`foreigenKey` (DDL 관련)

- 외래 키 제약조건을 직접 지정
- 테이블 생성(ddl-auto create)시에만 사용

`unique`, `nullable`, `insertable`, `updatable`, `columnDefinition`, `table`

- @Column 어노테이션 속성과 같다.

#### 예시
```java
@Entity
@Table(name = "players")
public class Player {
    ...

    @ManyToOne
    @JoinColumn(name = "team_id") // 참조 필드를 players 테이블의 FK인 team_id 컬럼과 매핑
    private Team team;

    ...    
}
```

#### 생략할 경우
- 기본 전략을 사용한다.
	- 기본 전략: `필드명 + _ + 참조하는 테이블의 PK 컬럼명` 이름에 해당하는 외래키와 매핑한다. 

```java
@Entity
@Table(name = "players")
public class Player {
    ...

    @ManyToOne
    private Team team; // team_team_id FK와 매핑 (team 테이블의 PK 컬럼명이 team_id라고 가정하면)

    ...    
}

```