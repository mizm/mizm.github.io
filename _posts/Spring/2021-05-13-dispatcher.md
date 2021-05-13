---
layout: post
title:  "Spring Mvc DispatcherServlet"
date:   2021-05-13T10:02:52-05:00
author: miz
categories: Spring
---
> 김영한님의 인프런 강의 https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1 를 보고 정리한 내용입니다.

# Spring DispatcherServlet

# 스프링 MVC의 프론트 컨트롤러 패턴
- 프론트 컨트롤러 패턴이란
    - 기존 servlet 처럼 클라이언트 호출이 특정한 Servlet Controller를 호출 하는 것이 아닌 공통의 서블릿으로 요청을 받는 방법
    - 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출해준다.
- 장점
    - 입구가 하나 가 된다.
    - 공통 처리가 가능하다
    - 프론트 컨트롤러를 제외한 나머지 컨트롤러는 서블릿을 사용하지 않아도 된다.

- 스프링의 프론트 컨트롤러 DispatcherServlet
![dispatcher](/assets/images/dispatcherservlet.PNG)

## 동작 순서
1. 핸들러 매핑 : 요청 URL에 매핑된 핸들러를 조회한다.
    - 핸들러 목록에서 URL을 호출 할 수 있는 핸들러를 찾기 위해 존재한다.
    - 핸들러 매핑을 순서대로 실행하면서 핸들러를 찾는다.
    - org.springframework.web.servlet.HandlerMapping 를 사용한다.
        - RequestMappingHandlerMapping : @RequestMapping에서 사용
        - BeanNameUrlHandlerMapping : 스프링 빈의 이름으로 핸들러를 찾는다.
2. 핸들러 어댑터 조회 : 핸들러를 실행 할 수 있는 핸들러 어댑터를 조회한다.
    - 다양한 종류의 컨트롤러를 호출 할 수 있는 핸들러 어댑터
    - 어댑터는 실제 컨트롤러를 호출하고, 그 결과로 모델엔 뷰를 반환해야한다.
    - 핸들러 어댑터를 순서대로 supports()를 호출해서 가능한지 여부 확인한다.
    - HadlerAdapter
        - RequestMappingHandlerAdapter : @RequestMapping에서 사용한다.
        - HttpRequestHandlerAdapter : HttpRequestHandler에서 사용한다.
        - SimpleControllerHandlerAdapter : Controller 인터페이스(애노테이션X, 과거에 사용) 처리
3. 핸들러 어댑터 실행 : 핸들러 어댑터를 실핸한다.
    - 실제 컨트롤러 호출
4. 핸들러 실행 : 핸들러 어댑터가 핸들러(컨트롤러)를 실행한다.
5. ModelAndView : 핸들러가 반환한 값을 핸들러 어댑터가 ModelAndView로 변환해서 반환한다.
6. viewResolver 호출 : 뷰 리졸버를 찾고 실행한다.
    - 핸들러가 반환한 뷰의 논리 이름을 통해서 viewResolver를 순서대로 호출한다.
    - 뷰리졸버 종류
        - BeanNameViewResolver : 빈 이름으로 뷰를 찾아서 반환한다. (예: 엑셀 파일 생성 기능에 사용)
        - InternalResourceViewResolver : JSP를 처리할 수 있는 뷰를 반환한다.
7. View 반환 : 뷰 리졸버는 논리 view의 이름을 물리 이름으로 바꾸고, 렌더링을 담당하는 View 객체를 반환한다.
8. View 렌더링
    
