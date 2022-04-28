---
emoji: 🎉
title: Spring Framework 정리
date: '2021-04-26 01:00:00'
author: 도리니
tags: spring
categories: 알쓸개잡 featured
---

1. Spring Framework란?
    - Spring Framework란 Java 엔터프라이즈 개발을 편하게 해주는 오픈소스 경량급 애플리케이션 프레임워크입니다.    
        - 애플리케이션 프레임워크 : 특정 분야에 국한 되지 않고 전 영역을 포괄하는 범용적인 프레임워크를 말한다.
        - 경량급 프레임워크 : 단순한 웹컨테이너에서도 엔터프라이즈 개발의 고급기술을 대부분 사용할 수 있다. 
        - 엔터프라이즈 개발 : 개발자가 복잡하고 실수하기 쉬운 low level에 많이 신경쓰지 않으면서, Business Logic 개발에 전념할 수 있도록 해줍니다.
    - Spring Framework의 특징
        - 컨테이너 역할 : Spring 컨테이너는 Java 객체의 생명주기를 관리하며, Spring 컨테이너로부터 필요한 객체를 가져와서 사용할 수 있다.
        - DI (의존성 주입) : Spring은 설정파일이나 어노테이션을 통해서 객체간의 의존관계를 설정할 수 있도록 한다.
        - AOP 지원 : 트랜잭션이나 로깅, 보안과 같이 공통적으로 필요로하는 모듈들을 실제 핵심모듈에서 분리해서 적용할 수 있다.
        - POJO 지원: Spring 컨테이너에 저장되는 Java 객체는 특정한 인터페이스를 구현하거나, 특정 클래스를 상속받지 않아도 된다.
        - 트랜잭션 처리를 위한 일관된 방법을 지원 : JDBC 등 어떤 트랜잭션을 사용하던 설정을 통해 정보를 관리하므로 트랜잭션 구현에 상관없이 동일한 코드 사용 가능 (선언적)
        - 영속성(Persistence)과 관련된 다양한 API지원 : Mybatis, Hibernate등 데이터베이스 처리를 위한 ORM 프레임워크들과 연동 지원
    - Spring Framework 기능 요소
        - Spring Core : Spring Framework의 기본 기능 제공. 이 모듈에 있는 Bean Factory는 Spring의 기본 컨테이너면서 스프링 DI의 기반이다.
        - Context : Context모듈은 BeanFactory의 개념을 확장한 것으로 국제화 메시지, 애플리케이션 생명주기 이벤트, 유효성 검증등을 지원한다.
        - DAO : DAO 패키지는 JDBC에 대한 추상화 계층으로 JDBC 코딩이나 예외처리하는 부분을 간편화 시켰으며, AOP 모듈을 이용해 트랜잭션 관리 서비스도 제공한다.
        - ORM : 널리 사용되는 ORM 프레임워크와의 연결고리를 제공한다. ORM제품들을 Spring의 기능과 조합해서 사용할 수 있도록 해준다.
        - AOP : AOP모듈을 통해 Aspect 지향 프로그래밍을 지원한다.
2. AOP란 무엇인가요?

    관점지향 프로그래밍이라는 뜻으로, 핵심적인 기능에서 부가적인 기능을 분리하는 것입니다. 분리한 부가기능을 애스팩트라는 모듈형태로 만들어서 설계하고 개발하는 방법입니다.

    핵심기능에서 부가기능을 분리함으로 써, 핵심기능을 구현할 때 객체지향적인 가치를 지킬 수 있도록 도와주는 개념입니다.

    - 그럼 애스팩트란 무엇인가요?

        부가기능(=공통기능)을 정의한 코드인 어드바이스와 어드바이스를 어디에 적용할 지 결정하는 포인트컷을 합친 개념이다.

        Target을 호출하는 이벤트 발생 시, Advice type에 따라 시기에 맞추어 Runtime을 가로채서 Advice가 실행되도록 한다. 

    - AOP 용어
        - 타겟 (Target)  : 핵심기능을 담고 있는 모듈로, 타겟은 부가기능을 부여할 대상이된다.
        - 어드바이스(advice) : 어드바이스는 타겟에 제공할 부가기능을 담고 있는 모듈이다.
        - 조인포인트(join point) : 어드바이스가 적용될 수 있는 위치를 말한다. 타겟이 구현한 인터페이스의 모든 메소드는 조인포인트가 된다.
        - 포인트컷 (Point Cut): 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식이다.
        - 애스팩트 (Aspact) : AOP의 기본 모듈이다. (어드바이스+포인트컷), 싱글톤 형태
        - 어드바이저 (Advisor) :  어드바이저 = 애스팩트, 스프링AOP에서만 사용되는 용어
        - 위빙(Weaving) : 포인트컷에 의해서 결정된 타겟의 조인포인트에 부가기능을 삽입하는 과정, 핵심기능(타겟)에 영향을 주지 않으면서 필요한 부가기능을 추가할 수 있도록 해주는 핵심적인 처리과정이다.
    - AOP 특징
        1. Spring은 프록시 기반 AOP를 지원한다.
            - Spring은 타겟 객체에 대한 프록시를 만들어 제공한다.
            - 타겟을 감싸는 프록시는 실행시간(Runtime)에 생성된다.
            - 프록시는 어드바이스를 타겟 객체에 적용하면서 생성되는 객체이다.
        2. 프록시가 호출을 가로챈다. (Intercept)
            - 프록시는 타겟 객체에 대한 호출을 가로챈 다음 어드바이스 타입(before, after, after throwing, after returning, after around)에 맞게 부가기능 로직 수행 후 핵심기능 로직을 호출한다.
        3. Spring AOP는 메서드 조인포인트만 지원한다.
            - Spring은 동적 프록시를 기반으로 AOP를 구현하므로 메서드 조인 포인트만 지원한다. (런타임 시점에만 지원한다) 그런데 AspectJ와 같은 고급 AOP프레임워크를 사용하면 다양한 작업에 부가기능을 사용할 수 있다. (객체의 생성, 필드값의 조회와 조작 등)

    - 구현방식
        - XML 기반의 POJO 클래스를 이용한 AOP 구현

                Advice 클래스 작성 후, xml설정파일에 <aop:config> 로 애스펙트 설정

        - @Aspect 어노테이션을 이용한 AOP 구현
            - Advice 종류
                - Around : Join point 앞 뒤로 실행
                - Before : Join point 이전 시점 , After : Join point 이후 시점
                - After Returning : Join point 메서드 호출이 정상적으로 종료된 뒤에 실행되는 Advice
                - After Throwing : Join point호출 후 Exception이 발생할 때 실행되는 Advice

        - Join point 인터페이스 (Advice 클래스)
            - Around 어드바이스는 join point의 하위 클래스인 ProceedingJoinPoint 타입의 파라미터를 필수적으로 선언해야한다.
        - Point cut 표현식 문법 대표적인 사용은 excecution()이다.
            ```jsx
            excecution([접근제한자 패턴(생략가능)] 리턴타입패턴 [타입패턴.] 
            이름패턴 (타입패턴| "..",..) [throws 예외패턴])

            예시)
            excecution(* myspring.user.service.UserServiceImpl.*(..))

            ```
    - 스프링 트랜잭션
        - 선언적 트랜잭션 :  어노테이션(Xml로 설정)  AOP를 이용한 선언적 방식
    - MVC 패턴
        - MVC는 Business logic과 presentation logic을 분리하여 적용하는 패턴이다.
        - 모델 : 비즈니스 로직 및 데이터 처리 담당 (DAO, Service)
        - 뷰 : 모델이 처리한 데이터나 작업결과를 출력하는 화면(Html, jsp)
        - 컨트롤러 : 클라이언트 요청을 받았으때 그 요청에 대해 실제 업무를 수행하는 모델 컴포넌트를 호출함 (Servlet , JSP)

    - 모델1 : Controller 역할을 JSP가 담당함
    - 모델2 : Controller 역할을 Servlet에서 담당함
    - Front Controller 패턴 : 클라이언트가 보낸 요청을 받아서 공통적인 작업을 먼저 수행 (인증 or 권한체크) - Dispatcher Servlet
    - 흐름 : Dispatcher Servlet → Handler Mapping → Controller → ModelAndView → View Resolver → View
    