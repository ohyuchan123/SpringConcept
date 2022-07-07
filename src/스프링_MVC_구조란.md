# Spring 개념 정리
### Spring MVC 구조란?

#### 스프링 프레임워크는 <span style="color:#9370DB">MVC 구조</span>로 이루어져있다.

```
▶ MVC 구조란?
    Model - View - Controller의 줄임말
```

Spring의 구조를 살펴보면 아래와 같다.

- View-Controller-Service-Serviceimpl-DAO-DAOimpl-DTO   
      각 구조에 대해 보면 크게 View,Controller,Service,DAO,DTO로 이루어져있다. 이 외에도 DispatcherServlet,
       servlet-context가 있지만 구조만 살펴본다.


- View  
      말 그대로 <span style="color:#9370DB">사용자에게 보여지는 화면</span>을 View라고 한다. spring에서는 JSP를 통해 화면을 구성하고 Controller를 통해 벡엔드 서버와 연결한다.


- Controller   
  <span style="color:#9370DB">View와 Service 사이를 연결</span>한다. 클라이언트에서 입력한 URL에 맞는 View를 보여주고, View에서 처리하는 데이터를 Service로 전달해준다.
```java
    @RequstMapping(value="/")
    public String home(){
        service.method();
            return "index";
    }// localhost:port/로 접속한 클라이언트에게 index.jsp를 반환한다.
```

- Service   
  <span style="color:#9370DB">실제 로직을 처리하는 곳</span>으로 모든 기능은 Service에서 만들어진다. Controller를 통해 화면과 연결되고, DAO를 통해 데이터베이스와 연결된다.


- DAO   
Data Access Object의 줄임말인 DAO는 <span style="color:#9370DB">프로젝트와 데이터베이스를 연결</span>한다. Mapper에 SQL을 명시한뒤 Mapper와 함께 데이터베이스와 데이터를 주고받는다.


- DTO   
Data Transfer Object의 줄이말이고 VO(Value Object)라고도 불리는 DTO는 MVC 구조 사이사이에서 <span style="color:#9370DB">데이터 교환을 위한 오브젝트</span>이다. 특이하게 getter/setter 두가지 함수만 가지고 있으며 주로 데이터베이스 테이블과 매칭된다.
  - DTO와 VO가 완벽하게 같은 말은 아니지만 크게 차이를 두지 않는다
```java
public class temp{ //데이터베이스 테이블 컬럼과 GETSET만 가지고 있다.
    private int id;
    private String name;
    
    public int getId(){return id;}
    public void setId(int id){this.id = id;}
    
    public String getName() {return name;}
    public void setName(String name) {this.name = name;}
}
```