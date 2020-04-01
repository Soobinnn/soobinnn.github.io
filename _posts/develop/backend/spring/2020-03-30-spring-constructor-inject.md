---
title: '[Spring] Constructor Inject'
date: 2020-03-30 13:59:00 -0400
categories: devlog
tags: spring devlog constructor inject
---

# Dependency Injection (의존관계 주입)

- Tight Coupling (강한 결합)

- Loosely Coupling (느슨한 결합)


## Loosely Coupling (느슨한 결합)

객체를 주입 받는 것은 외부에서 생성된 객체를 인터페이스를 통해 넘겨받는 것이다.

결합도를 낮출 수 있고, 런타임 시에 의존관계가 결정되기 때문에 유연한 구조를 가진다.


# 주입 방법

- Constructor Injection

- Setter Based Injection


## Constructor Based Injection

생성자 주입을 사용하게 되면 SOLID 원칙에서 Open Closed Principle을 지키기 위한 디자인 패턴 중 전략패턴을 사용하게 된다.

### Example
```java
public class Controller {
    private Service service;

    public Controller(Service service) {
        this.service = service;
    }

    public void callService() {
        service.doSomething();
    }
}
```
```java
public class Main {
    public static void main(String[] args) {

        // Controller controller = new Controller(); // 컴파일 에러

        Controller controller1 = new Controller(new ServiceImpl());
        Controller controller2 = new Controller(
            () -> System.out.println("Lambda implementation is doing something")
        );
        Controller controller3 = new Controller(new Service() {
            @Override
            public void doSomething() {
                System.out.println("Anonymous class is doing something");
            }
        });

        controller1.callService();
        controller2.callService();
        controller3.callService();
    }
}
```


## Setter Based Injection (수정자를 통한 주입)

### Example
```java
public class Controller {
    private Service service;

    public void setService(Service service) {
        this.service = service;
    }

    public void callService() {
        service.doSomething();
    }
}

```

```java
public interface Service {
    void doSomething();
}
```

```java
public class ServiceImpl implements Service {
    @Override
    public void doSomething() {
        System.out.println("ServiceImpl is doing something");
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Controller controller = new Controller();

        // 어떤 구현체이든, 구현체가 어떤방법으로 구현되든 Service 인터페이스를 구현하기만 하면 된다.
        controller.setService(new ServiceImpl1());
        controller.setService(new ServiceImpl2());

        controller.setService(new Service() {
            @Override
            public void doSomething() {
                System.out.println("Anonymous class is doing something");
            }
        });

        controller.setService(
          () -> System.out.println("Lambda implementation is doing something")
        );

        // 어떻게든 구현체를 주입하고 호출하면 된다.
        controller.callService();
    }
}
```

### Issue

수정자 주입으로 의존관계 주입은 런타임시에 할 수 있도록 낮은 결합도를 가지게 구현되었다.

하지만, 수정자를 통해서 Service의 구현체를 주입해주지 않아도 Controller 객체는 생성가능하다.

Controller 객체가 생성가능하다는 것은 내부에 있는 callService() 메소드도 호출 가능하다는 것인데, callService 메소드는 service.doSomething()을 호출하고 있으므로
NullPointerException이 발생한다.

`\* 주입이 필요한 객체가 주입이 되지 않아도 얼마든지 객체를 생성할 수 있다는 문제가 발생.`

이 문제를 해결 할 수 있는 방법이 Constructor Based Inject 이다.

### Constructor Based Injection 이점

1. null을 주입하지 않는 한 NullPointerException은 발생하지 않는다.

2. 의존관계 주입을 하지 않은 경우에는 Controller 객체를 생성 할 수 없다. 즉, 의존관계에 대한 내용을 외부로 노출시킴으로써 컴파일 타임에 오류를 잡아낼 수 있다.

3. final을 사용할 수 있다. final로 선언된 레퍼런스 타입 변수는 반드시 선언과 함께 초기화 되어야 하므로 setter 주입시에는 의존관계 주입을 받을 필드에 final을 선언할 수 없다. 

`\* final을 사용하면 Controller 내부에서 service객체를 바꿀 수 없다. -> 무결성`

# Spring에서 DI 
스프링에서 필드 주입은 수정자를 통한 주입과 유사한 방식으로 이뤄진다.

# Spring DI 주입 방법

- Constructor Injection

- Setter Based Injection

- Field Injection

## Field Inject
Field Inject의 단점은 스프링 컨테이너 말고 외부에서 주입할 수 있는 방법이 없다.

### Example
```java
@Service
public class StudentServiceImpl implements StudentService {

    @Autowired
    private CourseService courseService;

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }

}
```

## Setter Based Injection
스프링 컨테이너가 아닌 외부에서 수정자를 호출해서 주입할 수 있다.

```java
@Service
public class StudentServiceImpl implements StudentService {

    private CourseService courseService;

    @Autowired
    public void setCourseService(CourseService courseService) {
        this.courseService = courseService;
    }

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }
}
```

## Constructor Injection
```java
@Service
public class StudentServiceImpl implements StudentService {

    private final CourseService courseService;

    @Autowired
    public StudentServiceImpl(CourseService courseService) {
        this.courseService = courseService;
    }

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }
}
```

### Constructor Based Injection 이점

1. 순환 참조 방지

2. 테스트 용이

3. Immutable



## 테스트 용이
DI의 핵심은 관리되는 클래스가 DI 컨테이너에 의존성이 없어야 한다는 것이다. 즉, 독립적으로 인스턴스화가 가능한 POJO(Plain Old Java Ojbect) 여야 한다는 것이다. DI 컨테이너를 사용하지 않고서도 단위 테스트에서 인스턴스화할 수 있어야 한다.

생성자 주입을 사용하면 테스트 방법이 없다기보다는 조금 더 편리하다고 생각하면 좋을 것 같다. Mockito(@Mock과 @spy 같은)를 적절히 섞어서 테스트를 할 수 있지만 물론 아래처럼 생성자 주입을 사용한 경우 매우 간단한 코드를 만들 수 있다.

```java
SomeObject someObject = new SomeObject();
MadComponent madComponent = new MadComponent(someObject);
madComponent.someMadPlay();
```

## Immutable
필드 주입과 수정자 주입은 해당 필드를 final로 선언할 수 없다. 따라서 초기화 후에 빈 객체가 변경될 수 있지만 생성자 주입의 경우는 다르다. 필드를 final로 선언할 수 있다. 물론 런타임 환경에서 객체를 변경하는 경우가 있을까 싶지만 이로 인해 발생할 수 있는 오류를 사전에 미리 방지할 수 있다.

실행 중에 객체가 변하는 것을 막을 수 있다.

오류를 사전에 방지할 수 있다.


# 참고 문서
https://yaboong.github.io/spring/2019/08/29/why-field-injection-is-bad/

https://madplay.github.io/post/why-constructor-injection-is-better-than-field-injection

https://zorba91.tistory.com/238