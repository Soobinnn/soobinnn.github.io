---
title: '[Spring] JPA'
date: 2020-04-07 23:01:00 -0400
categories: devlog
tags: spring devlog jpa
---

# JPA (Java Persistence API)
![spring-jpa-0](/assets/img/post/spring/spring-jpa-0.PNG)

Java ORM 기술에 대한 표준 명세. Java에서 제공하는 API. 

Java 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스
(JPA는 인터페이스이다.(라이브러리 X))

기존 EJB에서 제공되던 엔티티 빈을 대체하는 기술

ORM이기 때문에 자바 클래스와 DB테이블을 매핑한다.

### 특징

객체를 통해 쿼리를 작성할 수 있는 JPQL(Java Persistence Query Language) 지원

JPA는 성능 향상을 위해 지연 로딩이나 즉시 로딩과 같은 몇가지 기법을 제공하는데,
이것을 잘 활용하면 SQL을 직접 사용하는 것과 유사한 성능을 얻을 수 있다.

### Why use

1. sql 중심 개발 -> 객체 중심 개발
  -> sql 코드 반복, 객체 지향과 관계지향 DB와 패러다임 불일치

2. 생산성 증가
  -> 간단한 메소드로 CRUD가 가능

3. 유지보수 쉽다
  -> 기존 : 필드 변경 시 모든 SQL을 수정
    JPA : 필드만 추가하면 된다.
  

# ORM
ORM (Object Relational Mapping)으로, RDB 데이터베이스 정보를 객체지향으로 손쉽게 활용할 수 있도록 도와주는 도구

Object(자바객체)와 Relation(관계형 데이터베이스) 간의 맵핑을 통해서 보다 손쉽게 적용할 수 있는 기술을 제공해준다.

쿼리에 집중하기 보다는 객체에 집중 함으로써, 조금 더 프로그래밍적으로 활용할 수 있다.

### Persistance Framework

JDBC프로그래밍의 복잡함이나 번거로움 없이 간단한 작업만으로 DB와 연동되는 시스템을 빠르게 개발할 수 있고 안정적인 구동을 보장

Persistance Framework는 SQL Mapper와 ORM으로 나눌 수 있다.

### ORM vs SQL Mapper

DB 테이블을 자바 객체로 매핑함으로써 객체간의 관계를 바탕으로 SQL을 자동으로 생성하지만, Mapper는 SQL을 명시해줘야함.

ORM은 RDB의 관계를 Object에 반영하는 것이 목적

Mapper는 단순히 필드를 매핑시키는 것이 목적

- SQL Mapper
SQL - mapping - Object 필드
SQL 문으로 직접 디비를 조작한다

Mybatis, jdbcTemplate


- ORM
DB 데이터 - maaping - Object 필드
객체를 통해 간접적으로 디비 데이터를 다룸
객체와 디비 데이터를 자동으로 매핑해줌
  - SQL 쿼리가 아니라 메소드로 데이터를 조작할 수 있음
  - 객체간 관계를 바탕으로 sql을 자동으로 생성
Persistant API

JPA, Hibernate


### JDBC

JDBC는 DB에 접근할 수 있도록 자바에서 제공하는 API

모든 Java Data Access 기술의 근간 -> 모든 Persistance Framework는 내부적으로 JDBC API를 이용

### Spring-data-jdbc

O/R Mapping
CrudRepository
Aggregates, References

No EntityManager(PersistenceContext)

No Caching
No Lazy Loading
No Dirty traacking
No Proxy

Spring Data JDBC는 간단한 컨셉을 가지고있음.

#### O/R Mapping

- Annotation

@Table : 메핑 테이블

@id : PK 컬럼 매핑

@Version : Version 컬럼 매핑

@Column : 컬럼 매핑 OneToOne

@Embedded : Embedded 객체 속성 컬럼 매핑

@MappedCollection : OneToMany 관계 매핑
  - idColumn : FK 컬럼 매핑 (default column name: "변수명")
  - keyColumn : OrderBy 컬러 매핑 (default column name: "변수명_KEY")

@PersistenceConstructor : 조회 결과 객체 복원 사용 생성자
  - 생성자가 한개만 존재한다면, 선언하지 않아도 된다

@ReadOnlyProperty : 읽기 전용 컬럼

@Transient : 컬럼 매핑 하지 않는다
  -@PersistenceConstructor 생성자 속성에 포함되면 안된다.

@AccessType : 매핑 대상을 FIELD / PROPERTY로 지정

- 특징

Value Object 지원(Immutable)

NamingStrategy 지원

상속/다형성 매핑 미지원
복합키 매핑 미지원
AttributeConverter 미지원

Spring Data JDBC 는 Entity 설계시 Aggregate 개념 적용을 강하게 주장함.

- AggregateRoot에 하나의 Repository 구성
  -> 하나의 집합체(Aggregate)는 하나의 Repository를 통해서 영속성을 관리함.

- OneToOne, OneToMany 매핑 지원
  -> FK는 연결 타겟 엔티티의 테이블에서 관리함.
  -> OneToMany 매핑시 Set Collection 타입이라면, @MappedCollection의 KeyColumn은 매핑 되지 않는다.
  -> 연관 관계 클래스에 @id는 선언하지 않아도 된다.(Table에 Column만 존재)

- ManyToOne, ManyToMany 미지원
  -> 집합체(Aggregate)의 개념에 위배되므로 향후에도 지원하지 않을 것으로 보인다.

- 양뱡향 연관관계 매핑 금지
  -> 양방향 관계 설정 시 대참사

- Aggregate 간의 관계는 Reference Id로 관리
  -> AggregateReference로 타입 지원 가능

@Embedded.Nullable 
: 객체 속성에 매핑되는 Column값이 모두 존재하지 않으면 Null로 복원

@Embedded.Empty
: 객체 속성에 매핑되는 COlumn값이 모두 존재하지 않으면, 빈 객첼 ㅗ복원

\* Embedded 클래스 설계 및 설정 전략
- 가능하면 Value Object(불변 객체)로 설계 (lombok: @Value)
- 모든 속성 컬럼이 NULLABLE 하다면, NoArgsConstructor를 제공하고 @Embedded.Empty를 선언한다.

- NOT-NULL컬럼이 존재한다면, AllArgsConstructor를 제공하고, @Embedded.Nullable을 선언

#### TypeConvertor

JDBC Driver에서 지원하지 않는 타입들은 Custom Converter를 작성해줘야함.

JPA의 AttributeConverter 미지원

#### DDL 관리
Hibernate와 같은 자동 DDL 생성 기능은 없기 때문에,
직접 DDL 을 정의하고 관리해야 함.
-> Liquibase / Flyway 같은 Schema 관리 솔루션 사용

### Spring-data-R@DBC


### Spring-data-jpa 

JPA는 ORM을 위한 자바 EE 표준이며 Spring-Data-JPA는 JPA를 쉽게 사용하기 위해 스프링에서 제공하고 있는 프레임워크

Spring-Data-JPA -> Hibernate -> JPA

Hibernate를 쓰는것과 Spring-Data JPA를 쓰는 것 사이에는 큰 차이가 없지만,

`구현체 교체의 용이성`, `저장소 교체의 용이성` 이라는 이유에서 Spring Data JPA를 사용하는 것이 좋음

Spring Data JPA, Spring Data MongoDB, Spring Data Redis 등 Spring Data 하위 프로젝트들은 findAll(), save()등을 동일한 인터페이스로 가지고 있기 때문에
저장소를 교체해도 기본적인 긴으이 변하지 않는다.

## Hibernate

Hibernate는 JPA 구현체의 한 종류이다.

JPA는 DB와 자바 객체를매핑하기 위한 인터페이스(API)를 제공하고 

JPA 구현체(Hibernate)는 이 인터페이스를 구현 한 것

Hibernate 외에도 EclipseLink, DataNucleus, OpenJPA, TopLink Essentials 등 있음.

![spring-jpa-2](/assets/img/post/spring/spring-jpa-2.PNG)

## Description

Hibernate가 SQL을 직접 사용하지 않는다고 해서 JDBC API를 사용하지 않는다는 것은 아님.

HQL(Hibernate Query Language)라 불리는 매우 강력한 쿼리 언어를 포함하고 있다.

  HQL은 SQL과 매우 비슷하며 추가적인 컨벤션을 정의할 수 있다.

  완전히 객체지향적이며 상속, 다형성, 관계등의 객체지향의 강점

  쿼리 결과로 객체를 반환하며 프로그래머에 의해 생성되고 직접적으로 접근할 수 있다.

  SQL에서는 지원하지 않는 페이지네이션이나 동적 프로파일링과 같은 향상된 기능을 제공

  여러 테이블을 작업할 때 명시적인 join을 요구하지 안흥ㅁ


JPA의 핵심 내용은 엔티티가 영속성 컨텍스트에 포함되어 있냐 아니냐로 갈린다.

JPA의 `엔티티 매니저`가 활성화된 상태로 트랜잭션 (@Transactional)안에서 DB에서 데이터를 가져오면 이 데이터는 `영속성 컨텍스트`가 유지된 상태이다.
이 상태에서 해당 데이터 값을 변경하면 트랜잭션이 끝나는 시점에 해당 테이블에 변경 내용을 반영하게 된다.

따라서 엔티티 객체의 필드값만 변경해주면 별도로 update쿼리를 날릴 필요가 없게 된다. -> 더티 체킹

> 영속 컨텍스트 : 엔티티를 담고 있는 집합. JPA는 영속 컨텍스트에 속한 엔티티를 DB에 반영한다. 엔티티를 CRD 하게되면 컨텍스트의 내용이 DB에 반영된다.
영속 컨텍스트는 직접 접근이 불가능하고 Entity Manager를 통해서만 접근이 가능하다.


### JPA 성능 최적화

1. 모아서 쓰는 버퍼링 기능
2. 읽을 때 쓰는 캐싱 기능

\* JPA도 JDBC API - DB 사이에 존재하기 때문에 위의 두 기능이 존재

#### 캐싱 

같은 트랜잭션 안에서는 같은 엔티티를 반환 - 약간의 조회 성능 향상 (크게 도움 X)
```java

String memberId = "100";
Member m1 = jpa.find(Member.class, memberId); // SQL
    
Member m2 = jpa.find(Member.class, memberId); // 캐시 (SQL 1번만 실행, m1을 가져옴)
    
println(m1 == m2) // true
```
결과적으로 SQL을 한번만 실행한다.

#### 버퍼링 기능
- Insert
```java
/** 1. 트랜잭션을 커밋할 때까지 INSERT SQL을 모음 */

transaction.begin(); // [트랜잭션] 시작

em.persist(memberA);

em.persist(memberB);

em.persist(memberC);

// -- 여기까지 INSERT SQL을 데이터베이스에 보내지 않는다.

// 커밋하는 순간 데이터베이스에 INSERT SQL을 모아서 보낸다. --

/** 2. JDBC BATCH SQL 기능을 사용해서 한번에 SQL 전송 */

transaction.commit(); // [트랜잭션] 커밋
```
1. 트랜잭션을 commit 할 때까지 INSERT SQL을 메모리에 쌓는다.
  
  이렇게 하지 않으면 DB에 INSERT Query를 날리기 위한 네트워크를 3번 타게 된다.

2. JDBC Batch SQL 기능을 사용해서 한 번에 SQL을 전송한다.

  JDBC Batch를 사용하면 코드가 굉장히 지저분해진다.

  지연 로딩 전략(Lazy Loading) 옵션을 사용한다.

- update
```java
/** 1. UPDATE, DELETE로 인한 로우(ROW)락 시간 최소화 */

transaction.begin(); // [트랜잭션] 시작

changeMember(memberA);

deleteMember(memberB);

비즈니스_로직_수행(); // 비즈니스 로직 수행 동안 DB 로우 락이 걸리지 않는다.

// 커밋하는 순간 데이터베이스에 UPDATE, DELETE SQL을 보낸다.

/** 2. 트랜잭션 커밋 시 UPDATE, DELETE SQL 실행하고, 바로 커밋 */

transaction.commit(); // [트랜잭션] 커밋
```
1. UPDATE, DELETE로 인한 ROW Lock 시간 최소화
2. 트랜잭션 커밋 시 UPDATE, DELETE SQL실행하고, 바로 커밋

##### Lazy Loading (지연 로딩)

```java
Meber meber = memberDAO.find(meberId);   // SELECT * FROM MEMBER
Team team = meber.getTeam();
String teamName = team.getName(); // SELECT * FROM TEAM
```
객체가 실제로 사용될 때 로딩하는 전략

memberDAO.find(memberId)에서는 Member 객체에 대한 SELECT 쿼리만 날린다.

Team team = member.getTeam()로 Team 객체를 가져온 후에 team.getName()처럼 실제로 team 객체를 건드릴 때

즉, 값이 실제로 필요한 시점에 JPA가 Team에 대한 SELECT 쿼리를 날린다.

Member와 Team 객체 각각 따로 조회하기 때문에 네트워크를 2번 타게 된다.

** Member를 사용하는 경우에 대부분 Team도 같이 필요하다면 즉시 로딩을 사용한다.

##### 즉시 로딩
JOIN SQL로 한번에 연관된 객체까지 미리 조회하는 전략

```java
Meber meber = memberDAO.find(meberId);  // SELECT M.*, T.* FROM MEBER JOIN TEAM ...
Team team = meber.getTeam();
String teamName = team.getName(); 
```
Join을 통해 항상 연관된 모든 객체를 같이 가져온다.

**애플리케이션 개발할 때는 모두 지연로딩으로 설정한 후에, 성능 최적화가 필요할 때 옵션을 변경하는 것을 추천

### Annotation

- @Entity
JPA에서는 테이블을 자동으로 생성해주는 기능 존재

DB Table == JPA Entity

Identify로 구분되는 객체

- @Table

실제 DB 테이블을 이름을 명시

- @Id
Index Primary Key를 명시

- @Column
실제 DB 컬럼명 명시

- @GeneratedValue
Prmary key 식별키 전략 설정


### Interface

#### Repository
![spring-jpa-1](/assets/img/post/spring/spring-jpa-1.PNG)


- CrudRepository 

  CRUD 관련 기능들을 제공

- PagingAndSortingRepository

  페이징 및 sorting 관련 기능들 제공

- JpaRepository

  JPA 관련 특화 기능들 (flushing, 배치성 작업) 기능 제공




## Get Start
build.gralde
```java
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
```

interface에 CrudRepository<T, ID>를 상속을 받는다.

```java
import org.springframework.data.repository.CrudRepository;

public interface UserRepository extends CrudRepository<User, Long> {
    User findUserByBoard(Long boardId);
}
```

\* Optional

Java8부터 추가된 타입.

Null을 처리하지 않고 해당 타입이 있나 없나로 직접 구분할 수 있도록 만들어진 타입. Null Point 익셉션에 대한 문제를 해결해줌.



## Spring Data JPA

### Before
```java
@Component
public class BoardRepositoryImpl implements BoardRepository {

  List<Board> boards = new ArrayList<>();

  public BoardRepositoryImpl() {
    boards.add(new Board(1004L, "Hello", "hi", 0L));
    boards.add(new Board(2020L, "boards", "hi", 0L));
  }

  @Override
  public List<Board> findAll() {
    return boards;
  }

  @Override
  public Optional<Board> findById(Long boardId) {
    return boards.stream()
        .filter(board -> board.getBoardId().equals(boardId))
        .findFirst()
        .orElse(null);
  }

  @Override
  public Board save(Board board) {
    board.setBoardId(1234);
    boards.add(board);
    return board;
  }
}
```

## 관계


## 참고자료
- jpa

https://velog.io/@adam2/JPA%EB%8A%94-%EB%8F%84%EB%8D%B0%EC%B2%B4-%EB%AD%98%EA%B9%8C-orm-%EC%98%81%EC%86%8D%EC%84%B1-hibernate-spring-data-jpa