---
title: '[Spring] Lombok '
date: 2020-02-03 12:51:00 -0400
categories: devlog
tags: spring devlog lombok boot
---

# Lombok 이란?
Lombok은 자바에서 @Getter, @Setter 같은 annotation 기반으로 관련 기존 DTO, VO, Domain Class 작성할 때, 멤버 변수에 대한 Getter/Setter Method, Equals(), hashCode(), ToString()과 멤버 변수에 값을 설정하는 생성자 등등을 자동으로 생성해 주는 라이브러리

## Get Start
build.gradle
```java
	compile "org.projectlombok:lombok:1.18.12"
	annotationProcessor "org.projectlombok:lombok:1.18.12"
```

## 왜 쓰는가?
### Before
```java

```

### After
```java
@ToString
@EqualsAndHashCode
@Getter @Setter
public class Student {
    private String id;
    private String name;

    public Student(){}

    public Student(String id, String name) {
        this.id = id;
        tihs.name = name;
    }
}
```

DTO를 보다 명시적으로 볼 수 있다.

## 장점

- 코드 작성이 쉽고 필요한 코드가 적다.
- 코드가 명시적이다.
- 수정이 간편하다.


## Lombok Annotation

- @Getter, @Setter
getter, setter 메소드를 자동으로 생성해줌.,
AccessLevel이라는 값을 가지고 있어, 이것을 통해 접근제한자를 설정해 줄 수 있다. (default Public)

- @ToString
toString() 메소드를 자동으로 생성해줍니다.

- @EqualsAndHashCode
equals(), hashCode()을 자동으로 생성해줍니다.

- @AllArgsConstructor
모든 인스턴스 변수를 포함하는 생성자를 생성해줌.

- @NoArgsConstructor
인자 없는 생성자 생성

- @RequriedArgsConstructor
필수 인자만 있는 생성자 생성(다른 생성자가 없을 때에만 만들어짐)

마찬가지로 AccessLevel이란 것을 포함하고 있어 접근제한자를 지정해줄 수 있다.

- @NonNull
해당 값이 Null 일 경우 NullPointerException을 발생

- @Data
@ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor 자동 생성

- @val
final 키워드 대신 사용하는 변수 선언

- @Value
불편 클래스를 쉽게 생성

- @Builder
Builder API처럼 사용 할 수 있도록 지원

- @SneakyThrows 
Exception 발생시 체크된 Throable로 감싸서 전달

- @Synchronized
메소드에 동기화 Lock을 설정

- @Log
종류별 로그를 사용할 수 있도록 한다.



## 주의사항
```java
//example
@Data
@Entity
@NoArgsConstructor
public class Sales {

  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  @ManyToOne
  @JoinColumn(name="owner_id", referencedColumnName = "id")
  private Owner owner;

  private long salesPrice;

  @OneToMany(fetch = FetchType.LAZY)
  @JoinColumn(name = "sales_id")
  private List<Payment> paymentList = new ArrayList<>();

  private LocalDateTime paymentDate;

  @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
  @CreationTimestamp
  private LocalDateTime createdDate;

  @JsonFormat(pattern = "yyyy-MM-dd HH:mm:ss")
  @UpdateTimestamp
  private LocalDateTime updatedDate;

  private String deleted;

}
```

1. @Data를 지양한다.
    -> 무분별한 Setter의 남용을 막고, 도메인 기능에 대한 메소드만 사용하도록

2. Entity는 지켜야할 고유의 영역이다.
    -> Entity를 변경하기 보다는 이 Entity를 사용하는 DTO를 사용하여 최대한 변경에 대응하기 쉽도록 한다.

3. JPA에서는 프록시를 생성하기 위해서 기본 생성자를 반드시 하나를 생성해야한다.
    -> 이때 접근 권한을 AccessLevel.PROTECTED설정하여 JPA에서의 Entity클래스 생성만 허용해준다.

```java
@Getter
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Sales extends AbstractTimeEntity {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private Long salesPrice;

    private LocalDateTime paymentDateTime;

    private Boolean deleted;

    @ManyToOne
    @JoinColumn(name="owner_id", referencedColumnName = "id")
    private Owner owner;

    @OneToMany(mappedBy = "sales", cascade = CascadeType.ALL)
    @JoinColumn(name = "sales_id")
    private List<Payment> paymentList = new ArrayList<>();

...
}
```

# 참고 문서
https://galid1.tistory.com/531

https://kwonnam.pe.kr/wiki/java/lombok/pitfall

https://woowabros.github.io/experience/2019/02/28/pilot-project-settle.html

https://cheese10yun.github.io/lombok/