# Spirng 개념 정리
### Ioc DI
##### 3.1 loc(Inversion of Control)

loC를 그대로 해석하면 제어의 역전이다. 무엇인가 제어하는 주체가 바뀐다는 의미인데 어떤   
제어가 어떻게 바뀌는 것일까?

Spring을 사용해 본 사람이라면 알듯이 Service, DAO 같은 객체를 사용자가 직접 생성(new)하지
않는다. @Autowired가 loc(제어의 역전)이다.

```java
//기존 자바 프로젝트
public class Order{
    private customer customer;
    
    public order(){
        this.customer = new customer();
    }
}
```


```java
//Spring 프로젝트
public class Order{
    @Autowired
    private cutomer cutomer;
}
```
스프링 컨테이너(loc container)는 프로젝트에서 사용되는 객체들을 Bean으로 관리하고 있고   
@Autowired를 통해 객체를 주입해준다.

기존엔 사용자가 생성(new)해 파라미터로 다른 객체로 보내거나 사용할 일이 없을 경우 객체를   
소멸하는 등 객체에 대한 제어를 직접 진행했다. 하지만 Spring에서는 위처럼 제어를 사용자가   
아닌 Spring Framework가 진행하기 때문에 제어의 역전이라고 표현한다.

```
Spring Bean
    spring에서 Bean은 스프링 프레임워크에 의해서 관리되는 자바 객체이다.
    
    ▶ Spring Bean은 Java Bean과 다른 의미이다.
```

#### 3.2 DI(Dependency Injection)
제 3자가 제어를 관리하는 순간 제어의 역전이고, 스프링이 생기기 전부터 있던 개념이었기에   
loc는 다른 프레임워크와 다른 스프링만의 차별점을 설명하기 부족했다. 그래서 스프링만의   
차별점을 설명하기 위해 만들어진 개념이 DI이다.

DI는 Spring에서 IoC 구조를 만드는 방식이다.   
DI를 그대로 해석하면 의존성 주입이다. 의존성은 무엇이고 왜 주입해야 할까? 프로그래밍에서   
뜻하는 의존성은 객체간의 관계를 먼저 알아야 이해하기 쉽다.

DI를 사용하는 이유는 객체간의 의존성을 줄이기 위함이다. 밖에서 객체를 생성해 넣어주기    
때문에 재사용이 늘어나고 수정에 용이해진다.
```java
// 기존 자바 프로젝트
class concept_api implements Post(){}
class concept_Spring implements Post(){}

class Blog_log() {
private Post post; // 블로그 글 클래스

  public Blog_log() {
  	this.post = new concept_api();
		this.post = new concept_Spring();
  }
}
```
```java
  // DI
  private Post post; // 블로그 글 클래스

    public Blog_log(Post post) {
    	this.post = new Post();
    }
```
만약 기존 프로젝트처럼 interface를 직접 만든다면 글마다 CRUD 함수가 필요하지만 DI처럼   
의존성을 주입해 사용한다면 Blog_log 하나의 클래스 만으로 모든 글을 관리할 수 있다.