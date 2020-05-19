---
title: '[Spring] Mokito'
date: 2020-05-18 15:08:00 -0400
categories: devlog
tags: spring devlog mokito test
---

# Mokito

Unit Test를 위한 java mocking Framework.
[http://mockito.org/](http://mockito.org/)

### Mock()
mock()메소드는 mock객체를 만들어서 반환함.

```java
@Test
public void example(){
    Board board = mock(board.class);
    assertTrue( board != null );
}
```

### @Mock
mcok()메소드 외에 annotation을 사용하여 선언할 수 있다.

`MockitoAnnotations.initMocks(this);`을 이용하여 @Mock 선언된 변수들을 객체로 만들어냄
```java
@Mock
Person p;

@Test
public void example1(){
    MockitoAnnotations.initMocks(this);
    assertTrue(p != null);
}
```

### When()

특정 목 객체를 만들었다면 이 객체로 부터 조건을 지정할 수 있다.

```java
@Test
public void example(){
    Person p = mock(Person.class);
    when(p.getName()).thenReturn("JDM");
    when(p.getAge()).thenReturn(20);
    assertTrue("JDM".equals(p.getName()));
    assertTrue(20 == p.getAge());
}
```

매개변수가 어떤 값이라도 관계 없다면 `any...`로 시작하는 메소드를 사용. 만약 특정 값을 넣어야 한다면 `eq()`
```java
public List<String> getList(String name, int age){ // do something code }

when(mockIns.getList(anyString(), anyInt()))
    .thenReturn(
        new ArrayList<String>(){
            { this.add("JDM"); this.add("BLOG"); }
        }
    );
```

### doThrow()

예외를 던지고 싶을떄 사용함.
```java
@Test(expected = IllegalArgumentException.class)
public void example(){
    Person p = mock(Person.class);
    doThrow(new IllegalArgumentException()).when(p).setName(eq("JDM"));
    String name = "JDM";
    p.setName(name);
}
```

### doNothing()
void 선언된 메소드에 when()을 사용 할떄
```java
@Test
public void example(){
    Person p = mock(Person.class);
    doNothing().when(p).setAge(anyInt());
    p.setAge(20);
    verify(p).setAge(anyInt());
}
```

### verify()

해당 구문이 호출 되었는지를 체크함. 단순한 호출뿐만 아니라 횟수나 타임아웃 시간까지 지정해서 체크해 볼 수 있다.

### @InjectMocks
클래스 내부에 다른 클래스를 포함하는 경우에 사용

```java

```

### @Spy
@Spy로 선언된 목 객체는 목 메소드를 별도로 만들지 않는다면 실제 메소드가 호출됨.
```java
Person p = spy(Person.class);
or
Person p = spy(new Person());
or
@Spy Person p;
```


## 참고 문서

https://jdm.kr/blog/222