## ch45_스프링JAP의 OSIV전략
### 2022.06.30

#### ✔ 영속성 컨텍스트, 트랜잭션 JDBC커넥션의 시작, 종료위치 변경
![image](https://user-images.githubusercontent.com/97611103/176588748-278f0cdf-8424-4dc6-b77a-09673d3fb924.png)

 - 세션의 시작은 **서블릿이 시작(Reaquest)**되는 시점(세션은 영속성 컨텍스트를 포함)
 - 트랜잭션, JDBC 커넥션의 시작은 **서비스레이어**
 - 트랜잭션, JDBC 커넥션의 종료는 **서비스레이어**
 - 세션은 컨트롤러 영역까지 끌고 가기 때문에 영속성이 보자오디어 select가 가능해지고 **lazy-loading**이 가능해진다.
	![image](https://user-images.githubusercontent.com/97611103/176588415-3943c028-6518-43b0-a229-5c9ecd4d29a5.png)

#### ✔ OSIV(Open Session In View)전략
 - 영속성 컨텍스트를 뷰까지 열어두는 기능
 - 뷰까지 영속성 컨텍스트가 살아있다면 뷰에서 지연로딩을 사용할 수 있다.
 - Spring Boot 2.0 이상에서는 open-in-view의 default가 true이다.
 ```
 장점 : View Template이나 API컨트롤러에서 지연로딩이 가능하다.
 단점 : 너무 오랜시간동안 JDBC 리소스를 사용하기 때문에 실시간 트래픽이 중요한 애플리케이션에서는 커넥션이 모자랄 수 있다.
 ```


#### ✔참고
 - https://getinthere.tistory.com/20