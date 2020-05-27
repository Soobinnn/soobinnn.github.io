---
title: '[Spring] data'
date: 2020-05-27 15:12:00 -0400
categories: devlog
tags: spring devlog bean data 
---


- Java Beans

- VO

- DTO

- Entity

## Java Beans
[Java Beans Spec](https://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html)

현재 이 스펙을 다 의식하고 개발하는 사람은 거의 없음.

getter/setter는 많은 프레임워크에서 활용되고 있음.

/* 그 역할을 하는 객체가 Setter가 꼭 있어야하는 것은 아니다.

## DTO (Data Transfer Object)

원격 호출을 효율화하기 위해 나온 패턴

네트워크 전송 시의 Data holder 역할로 쓰이는 느낌

해결하는 문제와 맥락이 달라졌는데 같은 패턴의 이름을 사용 가능한가?

레이어 간의 경계를 넘어서 데이터를 전달하는 역할은 과거와 동일하다고 생각할 수 있음.

원격 호출 레이어에 국한 되지 않게 쓰는 경우도 넓게 보면 이 용어로 이해할만 함.

다만 다양한 객체의 역할을 다 DTO로 이름 붙이는 건 혼란도 있음.

## VO (Value Object)

값이 같으면 동일하다고 간주되는, 식별성이 없는 작은 객체

DTO와 혼용해서 쓰여 왔다.

Data Holder의 의미로 폭넓게 생각하는 경향도 있음.

## Entity

사전적 의미 : 실체. (Something that exists apart from other things, having its own independent existence)

DB 테이블과 대응되는 객체

DDD의 용어

Entity : 연속성과 식별성의 맥락에서 정의되는 객체

Value Object : 식별성 없이 속성만으로 동일성을 판단하는 객체

### ENTITY를 감추기

#### ENTITY가 View, API 응답에 바로 노출될 때의 비용

- 캡슐화를 지키기 어려워진다.
  : 꼭 필요하지 않는 속성도 외부로 노출되어 향 후 수정하기 어려워진다.

- JSP, Freemarker에서의 ENTITY 참조
  : 파일 시점의 검사 범위가 좁다. -> ENTITY클래스를 수정했을 때 뷰에서 에러가 나는 경우가 뒤늦게 발견됨.
  JPA를 쓴다면 `OpenEntityManagerInViewFilter`를 고려해야한다. 
  -> 초보 개발자는 쿼리가 실행되는 시점을 예상하지 못한다.

- JSON 응답
  : @JsonIgnore, @JsonView 같은 선언이 많아지면 JSON의 형태를 클래스만 보고 예측하는 난이도가 올라간다.

#### 외부 노출용 DTO를 따로 만들기

- ENTITY -> DTO 변환 로직은 컴파일 타임에 체크된다.

- DTO는 비교적 구조를 단순하게 가져갈 수 있다.
  : 더 단순한 JSON 응답, JSP에서 쓰기 좋은 구조를 만들기에 유리하다.

- DTO의 변화는 외부 인터페이스로 의식해서 관리하는 범위가 된다.

- 여러 ENTITY를 조합할 수 있는 여지가 생긴다.

#### DTO 이름 고민

역할 별로 구분된 DTO 정의 예

- 이슈 조회 JSON 응답 : IssueResponse, IssueDto, IssueDetailDto
- 이슈 생성 JSON 요청 : IssueCreationRequest, IssueCreationCommand
- 이슈 조회 조건 : IssueQuery, IssueCriteria
- 이슈 DB 통계 조회 결과 : IssueStatsRow
- 이슈 + 코멘트 복합 조회 결과 : IssueCommentRow

### AGGREGATE로 ENTITY 간의 선긋기

#### AGGREGATE 란?

하나로 취급되는 연관된 객체군, 객체망
  - ENTITY와 Value Object의 묶음
  - 엄격한 데이터 일관성, 제약사항이 유지되어야 할 단위
  - Transaction, Lock의 필수 범위
  - 불변식(Invariants, 데이터가 변경될 때마다 유지되야 하는 규칙)이 적용되는 단위
  - Document DB와 어울림

AGGREGATE 1개당 REPOSITORY 1개
  AGGREGATE ROOT를 통해서 밖에서 AGGREGATE안의 객체로 접근함

Spring Data의 CrudRepository 인터페이스도 AGGREGATE 관점으로 보는 것이 좋음.

```java
public interface CrudRepository<AGGREGATE_ROOT, ID> extends Repository<AGGREGATE_ROOT, ID> {
  Optional<AGGREGATE_ROOT> findById(ID id);
  ...
}
```
#### AGGREGATE간의 경계가 있는 시스템

별도의 저장소나 API 서버를 분리할 때 상대적으로 유리

  - AGGREGATE밖은 EVENTUAL CONSISTANCY를 목표로 할 수도 있음
  - 여러 AGGREGATE의 변경은 Event, SAGA, TCC등의 패턴을 활용할 수도 있음.

AGGREGATE별로 Cache를 적용하기에도 좋음

분리할 계획이 없더라도 코드를 고칠 때 영향성을 파악하기가 유리

\* AGGREGATE 식별 시 주의점

CUD + 단순R (findById)에 집중
  - 모든 R을 다 포용하려고 한다면 깊은 객체 그래프가 나옴

(JPA를 쓴다면) Cascade를 써도 되는 범위인가?

#### AGGREGATE간의 참조

다른 AGGREGATE의 ROOT를 직접 참조하지 않고 ID로만 참조하기
```java
// before
public class Issue {
  private Repo repo;
}

// after

public class Issue {
  private long repoId;
}

public class Issue {
  private Association<Repo> repoId
}

public class Association<T> {
  private final long id;

  public Association(long id) {
    this.id = id;
  }
  ...
}

```
/* [Spring Data JDBC의 AggregateReference](https://github.com/spring-projects/spring-data-jdbc/blob/master/spring-data-jdbc/src/main/java/org/springframework/data/jdbc/core/mapping/AggregateReference.java)도 같은 역할

#### 여러 AGGREGATE에 걸친 조회

- Service 레이어에서 조합

```java
MilestoneEntity milestone = milestoneRepository.findByid(milestoneId);
int issueCount = issueRepository.countByMilestoneId(milestoneId)

var miletoneReponse  = MilestoneResponse.builder()
    .name(milestone.getName())
    .endedAt(milestone.endedAt())
    .issueCount(issueCount)
    .build();
```

DB 성능에 더유리 할 수 있음
 - 각각의 쿼리가 단순해짐
 - Application/DB 레벨의 캐쉬에 더 유리함.


- JOIN이 필수적인 경우

WHERE절에 따른 AGGREGATE 속성이 필요한 경우
```java
SELECT r.name, r.description, r.created_by, r.created_at
FROM repo r
    INNER JOIN account a ON a.id = r.created_by
WHERE a.email = :email
```
-> Repository에 조회조건 정도를 추가하고 Service단에서 다른 AGGREGATE를 다시 조합할 수도 있음

`List<Repo> findByCreatorEmail(String email)`

SELECT 결과까지 다른 AGGRAGATE의 속성을 포함할 경우
```java
SELECT r.name, r.description, a.name AS creator_name , a.email
FROM repo r
    INNER JOIN account a ON a.id = r.created_by
WHERE a.email = :email
```
전용 DTO를 만들 수 있다.
클래스가 늘어나지만 장점도 있음
-> Aggregate를 단순하게 유지할 수 있음.
-> JPA의 경우, Persistent Context를 의식하지 않아도 됨

이런 쿼리는 Repository보다는 DAO에 어울림

### REPOSITORY vs DAO

DAO는 퍼시스턴스 레이어를 캡슐화

DDD의 REPOSITORY는 도메인 레이어에 객체 지향적인 컬렉션 관리 인터페이스를 제공

> 개인적으로 TRANSACTION SCRIPT 패턴에 따라 도메인 레이어가 구성되고 퍼시스턴스 레이어에 대한 FAÇADE의 역할을 하는 객체가 추가될 때는 거리낌 없이 DAO라고 부른다.
<br/>도메인 레이어가 DOMAIN MDOEL 패턴으로 구성되고 도메인 레이어 내에 객체 컬렉션에 대한 인터페이스가 필요한 경우에는 REPOSITORY라고 부른다.
<br/>결과적으로 두 객체의 인터페이스의 차이가 보잘 것 없다고 하더라도 DAO가 등장하게된 시대적 배경과 현재까지 변화되어온 과정 동안 개발 커뮤니티에 끼친 영향력을 깨끗이 지워 버리지 않는 한 DAO와 REPOSITORY를 혼용해서 사용하는 것은 더 큰 논쟁의 불씨를 남기는 것이라고 생각한다




# 참고 문서
https://github.com/benelog/entity-dev/blob/master/src/index.adoc
