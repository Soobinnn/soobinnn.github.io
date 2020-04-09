---
title: '[Spring] JPA'
date: 2020-04-07 23:01:00 -0400
categories: devlog
tags: spring devlog jpa
---

# JPA (Java Persistence API)
ORM (Object Relational Mapping)으로, RDB 데이터베이스 정보를 객체지향으로 손쉽게 활용할 수 있도록 도와주는 도구

Object(자바객체)와 Relation(관계형 데이터베이스) 간의 맵핑을 통해서 보다 손쉽게 적용할 수 있는 기술을 제공해준다.

쿼리에 집중하기 보다는 객체에 집중 함으로써, 조금 더 프로그래밍적으로 활용할 수 있다.

## Hibernate
JPA에서 유명한 라이브러리


## Description
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
