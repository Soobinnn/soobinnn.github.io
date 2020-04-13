---
title: '[Spring] JPA'
date: 2020-04-07 23:01:00 -0400
categories: devlog
tags: spring devlog jpa
---

# JPA (Java Persistence API)

## Hibernate
JPA에서 유명한 라이브러리

- @Entity
Identify로 구분되는 객체

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