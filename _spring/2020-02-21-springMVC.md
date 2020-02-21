---
title: Spring MVC에 대한 이해
date: 2020-02-21
---
#### 1. MVC 패턴이란?
   * MVC 는 Model, View, Controller의 약자 입니다. 하나의 애플리케이션, 프로젝트를 구성할 때 그 구성요소를 세가지의 역할로 구분한 패턴입니다.
   * 사용자가 controller를 조작하면 controller는 model을 통해서 데이터를 가져오고 그 정보를 바탕으로 시각적인 표현을 담당하는 View를 제어해서 사용자에게 전달하게 됩니다.
--------------------------------------------------
#### 2. MVC 패턴에서 각 요소의 역할은?
   * Model에 대하여
      - 애플리케이션의 정보, 데이터를 나타냅니다. 데이터베이스, 처음에 정의하는 상수, 초기화값, 변수 등을 뜻합니다.
      - 또한 이러한 DATA, 정보들의 가공을 책임지는 컴포넌트를 말합니다.
      - 아래는 특징입니다.
         - 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다. 즉, 화면안의 네모박스에 글자가 표현된다면, 네모박스의 화면 위치 정보, 네모박스의 크기정보, 글자내용, 글자의 위치, 글자의 포맷 정보 등을 가지고 있어야 한다는 것입니다.
         - 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다. 데이터 변경이 일어났을 때 모델에서 화면 UI를 직접 조정해서 수정할 수 있도록 뷰를 참조하는 내부 속성값을 가지면 안 된다는 말입니다.
         - 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야만 한다. 모델의 속성 중 텍스트 정보가 변경이 된다면, 이벤트를 발생시켜 누군가에게 전달해야 하며, 누군가 모델을 변경하도록 요청하는 이벤트를 보냈을 때 이를 수신할 수 있는 처리 방법을 구현해야 합니다. 또한 모델은 재사용가능해야 하며 다른 인터페이스에서도 변하지 않아야 합니다.
         
   * View에 대하여
      - input 텍스트, 체크박스 항목 등과 같은 사용자 인터페이스 요소를 나타냅니다.
      - 다시 말해 데이터 및 객체의 입력, 그리고 보여주는 출력을 담당합니다.
      - 데이타를 기반으로 사용자들이 볼 수 있는 화면입니다.
      - 아래는 특징입니다.
         - 모델이 가지고 있는 정보를 따로 저장해서는 안된다. 화면에 글자를 표시 하기 위해, 모델이 가지고 있는 정보를 전달받게 될텐데, 그 정보를 유지하기 위해서 임의의 뷰 내뷰에 저장하면 안됩니다. 단순히 네모 박스를 그리라는 명령을 받으면, 화면에 표시하기만 하고 그 화면을 그릴 때 필요한 정보들은 저장하지 않아야 합니다.
         - 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 된다. 모델과 같은 자기 자신의 빼고는 다른 요소는 참조하거나 어떻게 동작하는지 알아서는 안됩니다. 그냥 뷰는 데이터를 받으면 화면에 표시해주는 역할만 가진다고 보면 됩니다.
         - 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다. 모델과 같이 변경이 일어났을 때 이른 누군가에게 변경을 알려줘야 하는 방법을 구현해야 합니다. 뷰에서는 화면에서 사용자가 화면에 표시된 내용을 변경하게 되면 이를 모델에게 전달해서 모델을 변경해야 할 것이다. 그 작업을 하기 위해 변경 통지를 구현합니다. 그리고 재사용가능하게끔 설계를 해야 하며 다른 정보들을 표현할 때 쉽게 설계를 해야 합니다.
   
   * Controller에 대하여
      - 데이터와 사용자인터페이스 요소들을 잇는 다리역할을 합니다.
      - 즉, 사용자가 데이터를 클릭하고, 수정하는 것에 대한 "이벤트"들을 처리하는 부분을 뜻합니다.
      - 아래는 특징입니다.
         - 모델이나 뷰에 대해서 알고 있어야 한다. 모델이나 뷰는 서로의 존재를 모르고, 변경을 외부로 알리고, 수신하는 방법만 가지고 있는데 이를 컨트롤러가 중재하기 위해 모델과 그에 관련된 뷰에 대해서 알고 있어야 합니다.
         - 모델이나 뷰의 변경을 모니터링 해야 한다. 모델이나 뷰의 변경 통지를 받으면 이를 해석해서 각각의 구성 요소에게 통지를 해야 합니다. 또한, 애플리케이션의 메인 로직은 컨트롤러가 담당하게 됩니다.
         
--------------------------------------------------
#### 3. 왜 MVC 패턴을 사용할까?
   - 사용자가 보는 페이지, 데이터처리, 그리고 이 2가지를 중간에서 제어하는 컨트롤, 이 3가지로 구성되는 하나의 애플리케이션을 만들면 각각 맡은바에만 집중을 할 수 있게 됩니다. 공장에서도 하나의 역할들만 담당을 해서 처리를 해서 효율적이게 됩니다.
   - 서로 분리되어 각자의 역할에 집중할 수 있게끔하여 개발을 하고 그렇게 애플리케이션을 만든다면, 유지보수성, 애플리케이션의 확장성, 그리고 유연성이 증가하고, 중복코딩이라는 문제점 또한 사라지게 되는 것입니다.  그러기 위한 MVC패턴입니다.

--------------------------------------------------
#### 4. MVC패턴 - Spring

   - Spring MVC 

      * Model
         * 애플리케이션의 상태(data)를 나타낸다.
         *  Java Beans

      *  View
         *  디스플레이 데이터
         *  Model data 렌더링을 담당하며, HTML output을 생성한다.
         *  JSP, Thymeleaf, Groovy,Freemarker등 여러 템플릿 엔진이 있다.

      *  Controller
         *  View와 Model 사이의 인터페이스 역할
         *  Model/View에 대한 사용자 입력 및 요청을 수신하여 그에 따라 적절한 결과를 Model에 담아 View에 전달한다.
         *  Model Object와 이 Model을 화면에 출력할 View Name을 반환한다.
         *  Controller -> Service -> Dao -> DB


   - Spring Framework가 제공하는 클래스

      *  DispatcherServlet
         *  스프링 프레임워크가 제공하는 Servlet 클래스
         *  사용자의 요청을 받는다.
         *  Dispatcher가 받은 요청은 HandlerMapping으로 넘어간다.

      *  HandlerMapping
         *  사용자의 요청을 처리할 Controller을 찾는다. (컨트롤러 URL Mapping)
         *  요청 url에 해당하는 Controller 정보를 저장하는 테이블을 가진다.
         *  클래스에 @RequestMapping("/url")annotation을 명시하면 해당 URL에 대한 요청이 들어왔을 때 테이블에 저장된 정보에 따라 해당 클래스 또는 메소드에 매핑한다.

      *  ViewResolver
         *  Controller가 반환한 View Name(the logical names)에 prefix, suffix를 적용하여 View Object(the physical view files)를 반환한다.
         *  예를 들어 view name: home, prefix: /WEB-INF/views/, suffix: .jsp는 “/WEB-INF/views/home.jsp”라는 위치의 View(JSP)에 Controller에게 받은 Model을 전달한다.
         *  이 후에 해당 View에서 이 Model data를 이용하여 적절한 페이지를 만들어 사용자에게 보여준다.
--------------------------------------------------
#### 5. 예제

```java
/**
 * Model 관련 예제
 * Controller 메서드에 input argument로 값을 넣어주면 Spring Frmework가 자동으로 Model을 만들어주고 해당 Model의 주  
 * 솟값만 넘겨준다.
 */
public String selectMember(HttpSession session, MemberVO membervo){
    MemberVO member = loginService.selectMember(membervo);
    if (null != member) {
        session.setAttribute("member", member);
        return "redirect:/insertPage";
    }
    return "redirect:/loginPage";
}
```

```java
<!-- View 관련 예제입니다.-->
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>로그인하세요</title>
</head>
    <body>
        <h1>로그인 하세요</h1>
        <hr>
        <form action ="/login" method="post">
            아이디:<input type="text" name="userID"><br>
            비밀번호:<input type="password" name="userPassword"><br>
            <input type="submit" value="로그인">
        </form>
    </body>
</html>
```

```java
/**
 * Controller 관련 예제입니다.
 * @Controller을 bean으로 등록하고
 * 해당 클래스가 Controller로 사용됨을 Spring Framework에 알림.
 * @Component -> @Controller, @Service, @Repository
 * 즉,  “/login” url로 HTTP GET 요청이 들어오면 login() 메서드가 실행된다.
 */
@PostMapping("/login")
public String selectMember(HttpSession session, MemberVO membervo){
    MemberVO member = loginService.selectMember(membervo);
    if (null != member) {
        session.setAttribute("member", member);
        return "redirect:/insertPage";
    }
    return "redirect:/loginPage";
}
```
--------------------------------------------------
#### 6. 각 Layer에 대한 설명
1. Controller
   - 클라이언트의 요청 (Request)을 어떻게 처리 할 지(Handling) 결정합니다.
   - 클라이언트의 Request가 서버에 도착했을 때 Controller에 정의 된 기준대로 요청을 처리합니다. 
   - 이를 위해 @Controller 라는 어노테이션을 명시합니다.  요청이 들어오면 @Controller의 내용을 기준삼아 요청을 처리하라는 뜻입니다.


2. Service

   - Service는 비지니스 로직이 들어가는 부분입니다. 
   - Controller가 Request를 받으면 적절한 Service에 전달하고, 전달 받은 Service는 비즈니스 로직을 처리합니다. 
   - DAO로 데이터베이스를 접근하고, DTO로 데이터를 전달받은 다음, 적절한 처리를 해 반환합니다.

3. DAO
   - Data Access Object의 줄임말입니다. 
   - DB를 사용해 데이터를 조회하거나 조작하는 기능을 담당합니다. 
   - 이렇게 따로 분리해놓는 이유는 HTTP Request를 Web Application이 받게 되면 Thread를 생성하게 되는데 비즈니스 로직이 DB로부터 데이터를 얻어오기 위해 매번 Driver를 로드하고 Connection 객체를 생성하게 되면 엄청 많은 커넥션이 일어나므로 DAO를 하나 만들어 DB 전용 객체로만 쓰는 것입니다. 
   - 이 개념은 DBCP(Database Connection Pool)로부터 나왔습니다. WAS(Web Application Server)이 실행되면 일정량의 DB Connection 객체를 Pool에다 저장해 두고, HTTP Request에 따라 필요할 때마다 Pool에서 Connection 객체를 가져다 쓰고 반환하는 것입니다.
