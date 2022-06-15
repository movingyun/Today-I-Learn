## ch18_User테이블 생성
### 2022.06.15

> **DTO - User**
```java
public class User {
	
	@Id//primary key 주기
	@GeneratedValue(strategy = GenerationType.IDENTITY) //프로젝트에서 연결된 DB의 넘버링 전략을 따라감.(=mySQL에서는 auto_increment를 사용하겠다!)
	private int id; //auto_increment
	
	@Column(nullable = false,length = 30) //Column어노테이션으로 컬럼 속성 준다(Notnull, 길이 = 30)
	private String username; //아이디
	
	@Column(nullable = false,length = 100) //Notnull, 길이 = 100
	private String password;
	
	@Column(nullable = false,length = 50) //Notnull, 길이 = 50
	private String email;
	
	@ColumnDefault(" 'user' ") //기본값 지정
	private String role; //Enum(값의 도메인을 정해둠)을 쓰는게 좋다. //admin,user,manager
	
	@CreationTimestamp //시간이 자동 입력
	private Timestamp createDate;
}
```

> **application.yml**
```java
    jpa:
    open-in-view: true 
    hibernate:
      ddl-auto: create // 프로그램이 시작될 때 테이블을 create하기(추후에 update로 바꿔줘야된다. 안바꿔주면 기존에 있던 table이 날라간다.)
      naming:
        physical-strategy: org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl //변수명 그대로 컬럼 생성(다른 속성을 주게되면 myEmail을 my_email로 만든다)
      use-new-id-generator-mappings: false 
    show-sql: true // console창에 작성된 sql문 보여주기
    properties:
      hibernate.format_sql: true
```