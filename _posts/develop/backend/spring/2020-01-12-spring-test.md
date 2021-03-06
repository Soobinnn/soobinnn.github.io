---
title: '[Spring] TEST'
date: 2020-01-12 20:39:00 -0400
categories: devlog
tags: spring devlog gradle tdd
---

# TEST 구성
## JUnit
java에서 독립된 단위 테스트 (Unit Test)를 지원해주는 프레임워크

> 단위 테스트(Unit Test) 란?

>> 소스코드의 특정 모듈이 의도된대로 정확히 작동하는지 검증하는 절차
>> 모든 함수와 메소드에 대한 테스트 케이스를 작성하는 절차

### 특징
assert 메소드로 테스트 케이스의 수행 결과를 판별
JUnit4부터는 테스트를 지원하는 어노테이션을 제공함 ex) @Test @Before @After)

@Test메소드가 호출할 때마다 새로운 인스턴스를 생성하여 독립적인 테스트가 이루어지게 한다.

### JUnit에서 지원하는 어노테이션
- @Test
: 테스트를 수행하는 메소드

JUnit은 각각의 테스트가 서로 영향을 주지 않고 독립적으로 실행됨을 원칙으로 @Test마다 객체를 생성한다.

이와 같은 Junit의 특성으로 인하여 ApplicationContext도 매번 새로 생성되기 때문에 테스트가 느려지는 단점이 있다.

- @Ignore
: 테스트를 실행하지 않게 된다.

- @Before
@Test 메소드가 실행되기 전에 반드시 실행된다.
공통으로 사용하는 코드를 사용

- @After
: @Test 메소드가 실행된 후 실행

- @BeforeClass
: @Test 메소드 보다 먼저 한번만 수행되어야 할 경우에 사용

- @AfterClass
: @Test 메소드 보다 나중에 한번만 수행되어야 할 경우에 사용

### 메소드
- assertEquals(a,b)
: 객체 a,b의 값이 일치함을 확인

- assertArrayEquals(a,b)
: 배열 a,b의 값이 일치함을 확인

- assertSame(a,b)
객체 a,b가 같은 객체임을 확인 (레퍼런스가 동일한가)

- asssertTre(a)
: 조건 a가 참인가 확인

-assertNotNull(a)
: 객체 a가 null이 아님을 확인

- aseertThat()
: Junit 4.4에서 추가
assertThat(T actual, Matcher<? super T> matcher) 형태로
첫번째 파라미터의 값을 뒤에 나오는 matcher라 불리는 조건으로 비교해서 일치하면 다음으로 넘어가고 아니면 테스트가 실패도록 함.

#### Macher
> hamcrest ?
>> 소프트웨어 테스트를 위한 framework
>> 
- is()
: matcher의 일종으로 equals로 비교해주는 기능을 가짐.
JUnit이 처음으로 의존성을 가지고 사용하는 제3자 클래스

다른 매쳐를 꾸며주는 용도로 사용. 매쳐에는 영향을 끼치지 않으며, 조금 더 표현력이 있도록 변경하여 준다

ex) assertThat("Simple Text", is(not("simpleText")));
위의 경우 is가 빠지더라도 문제없이 작동된다. 하지만 is가 있음으로써 쉽게 읽혀지는 테스트 코드가 된다.

- allOf
: 내부에 선언된 모든 matcher가 정상일 경우 통과

- anyOf
: 내부에 선언된 matcher 중 하나 이상 통과할 경우

- both
: both A and B 형식으로 matcher를 사용할 수 있게 해 준다.
A, B 매쳐 둘다 통과할 경우 테스트가 성공한다.

- either
: either A or B 형식으로 matcher를 사용할 수 있게 해 준다.
A, B 매쳐 둘중 하나가 성공할 경우 테스트가 성공한다.

- describedAs
: 매쳐내부의 메시지를 변경할 수 있다.

- everyitem
: 배열이나 리스트를 순회하며 매쳐가 실행된다.

- isA
: 비교되는 값이 특정 클래스일 경우 테스트가 통과된다.

- anything
: 항상 true를 반환하는 매쳐

- hasItem
: 배열에서 매쳐가 통과하는 값이 하나 이상이 있는지 여부를 검사한다.

- hasItems
: 배열에서 매쳐리스트에 선언된 값들 모두가 하나 이상 있는지 여부를 검사한다.

- equalTo
: 두 값이 같은지 여부를 체크한다. is와 동일하게 사용할 수 있다.

- any
: 비교값이 매쳐의 타입과 동일한지 여부를 체크한다. 

instanceOf와는 다르게 매쳐의 값은 앞서 비교값의 타입의 자식만 비교할 수 있다.

- instanceOf
: 비교값이 매쳐의 타입과 동일한지 여부를 체크한다. any와는 다르게 매쳐의 값은 비교값과 연관없는 경우에도 사용할 수 있다.

- not
: is와 동일하게 두가지 경우로 사용할 수 있다.
내부에 매쳐를 선언할 경우 내부 매쳐의결과를 뒤집는다

- nullValue
: 비교값이 null일경우 테스트가 통과한다.

- notNullValue
: 비교값이 null이 아닐경우 테스트가 통과한다.

- sameInstance
: 비교매쳐의 값과 같은 인스턴스일 경우 테스트가 통과한다. theInstance 와 동일

- theInstance
: 비교매쳐의 값과 같은 인스턴스일 경우 테스트가 통과한다. sameInstance 와 동일

- containsString
: 특정 문자열이 있는지를 검사한다.

- startsWith
: 특정 문자열로 시작하는지를 검사한다.

- endsWith
: 특정 문자열로 종료되는지를 검사한다.

### Spring Test에서 지원하는 어노테이션
- @RunWith(SpringJUnit4ClassRunner.class)
: JUnit프레임워크의 테스트 실행방법을 확장할 때 사용하는 어노테이션
어노태이션을 사용하면 JUnit에 내장된 러너를 사용하는 대신 어노테이션의 정의된 러너 클래스를 사용.

SpringJUnit4ClassRunner라는 클래스를 지정해주면 JUnit이 테스트를 진행하는 중에 ApplicationContext를 만들고 관리하는 작업을 해줌.

@RunWith 어노테이션은 각각의 테스트 별로 객체가 생성되더라도 Singleton의 ApplicationContext를 보장함.

한 클래스내에 여러개의 테스트가 있더라도 어플리케이션 컨텍스트를 초기 한번만 로딩하여 사용하기 때문에, 여러개의 테스트가 있더라도 처음 테스트만 조금 느리고 그 뒤의 테스트들은 빠르다.
(Junit은 각각의 테스트가 서로 영향을 주지 않고 독립적으로 실행됨을 원칙으로 하기에 @Test 마다 오브젝트를 생성한다.

이와 같은 Junit의 특성으로 인하여 ApplicationContext도 매번 새로 생성되기 때문에 테스트가 느려지는 단점이 있다.)

\* Junit5에선 @ExtendWith(SpringExtension.class)로 대체

- @ContextConfiguration
: 스프링 Bean 설정 파일의 위치를 지정할 떄 사용되는 어노테이션
 지정하지 않으면 테스트 클래스 파일이 있는 패키지 내에서 다음의 설정 파일을 사용한다. ContextConfigLocationTest-context.xml

- @Autowired
: 스프링 DI에서 사용되는 어노테이션
해당 변수에 자동으로 Bean을 매핑 해줌.
변수, setter메소드, 생성자, 일반메소드에 적용가능

- @SpringApplicationConfiguration
Spring Boot에서 class형태의 애플리케이션 컨텍스트를 로딩 할 수 있다.

# TEST 동작 방식
테스트 파일에는 @SpringBootTest 어노테이션이 붙어있는데 @SpringBootTest는 @SpringBootApplication이 붙어있는 스프링 메인 애플리케이션을 찾아간다.

메인에서 부터 시작하는 모든 Bean을 스캔을 한다.

테스트용 애플리케이션 context를 만들면서 모든 Bean을 등록 해준다.

그 후 MockBean을 찾아서 그 Bean만 교체해준다. 교체된 MockBean은 테스트마다 리셋된다.

## Mock
서블릿 컨테이너를 띄우지 않고
Mockup해서 서블릿을 Mocking한 것을 띄운다


# Test 종류
## 통합테스트
모든 Bean을 올려서 테스트
1. 쉽게 테스트 가능
2. 운영환경과 유사한 테스트
3. 전체적인 Flow 테스트 가능

단점
1. 모든 Bean을 올리기 떄문에 시간이 오래걸리고 무거움

2. 테스트 단위가 커서 실패시 디버깅 어려움
3. Rollback 처리가 안되는 테스트 진행을 하기 어려움

```java
@RunWith(SpringRunner.class)
@SpringBootTest(
  classes = {CommonConfig.class},
  properties = "classpath:application-test.yml"),
 webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT
)
@Transactional
public class IntegrationTest{
  
  @Autowired 
  MockMvc mvc;
  
  @Autowired
  private TestRestTemplate restTemplate;
  
}
```

## MockMvc

ajax, client 요청 내용을 controller에서 받아 처리하는 것과 같은 테스트

참고 [MockMvc Doc](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/web/servlet/MockMvc.html)

__.perform()__

ResultActions 인터페이스 리턴함.

```java
mvc.perform(get('/'))
mvc.perform(get('/').param('id','2'))
```

__ResultActions__

andExpect, andDo, andReturn 메소드 지원

[ResultActions](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/test/web/servlet/ResultActions.html)

- andExpert

assert 메소드와 유사
```java
.andExpect(status().isOk())
.andExpect(content().contentType("application/json;charset=utf-8")))
```

- andDo
요청에 대한 처리를 함.

```java
.andDo(print())
```

- andReturn
테스트한 결과 객체를 받를 때 사용


# TEST 예제

- Controller
- Service
- Repository

## Get Starting
### Contorller
__Code__
```java
package com.webatoz.backend.interfaces.board;

import com.webatoz.backend.domain.Board;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping(value = "/boards")
public class BoardController {

    @GetMapping
    public String list() {
        Board board = new Board(1L,"hi");
        return "hello";
    }
}
```
__Test Code__
```java
package com.webatoz.backend.interfaces.board;

import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.junit.jupiter.api.Assertions.*;

@RunWith(SpringRunner.class)
@WebMvcTest(BoardController.class)
class BoardControllerTest {
    @Autowired
    private MockMvc mvc;
    
    @Test
    public void 게시판조회() throws Exception {
        mvc.perform((get("/boards")))
                .andExpect(status().isOk());
    }
}
```

__@WebMvcTest(Controller.class)__

MVC를 위한 테스트, 웹에서 테스트하기 힘든 Controller를 테스트하는데 적합함.

웹상에서 요청과 응답에 대한 테스트 진행

Security 혹은 필터까지 자동으로 테스트하며 수동으로 추가/삭제 가능

@WebMvcTest 를 사용하면 MVC 관련된 설정인 @Controller, @ControllerAdvice, @JsonComponent, Filter, WebMvcConfigure, HandlerMethodArgumentResolver만 로드되기 때문에 @SpringBootTest보다 가볍게 테스트할 수 있다.





# 참고 문서
https://lalwr.blogspot.com/2019/09/spring-test.html

https://cheese10yun.github.io/spring-guide-test-1/


https://cheese10yun.github.io/spring-about-test/

https://itmore.tistory.com/entry/MockMvc-%EC%83%81%EC%84%B8%EC%84%A4%EB%AA%85

https://jdm.kr/blog/222