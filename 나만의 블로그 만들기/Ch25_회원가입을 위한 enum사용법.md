## ch25_회원가입을 위한 enum사용법
### 2022.06.22

> **RoleType**
```java
package com.cos.blog.model;

public enum RoleType {
 USER,ADMIN
}
```
#### ✔  enum 타입 사용
 - 값의 도메인을 지정해준다.
 - role에는 USER,ADMIN만 입력 받음!

> **DTO - User**
```java
//@DynamicInsert
public class User {

	//DB는 RoleType이 없어서 알려줘야댐
	@Enumerated(EnumType.STRING)
	private RoleType role; //Enum(값의 도메인을 정해둠)을 쓰는게 좋다. //admin,user

}
```
#### ✔  @DynamicInsert 어노테이션 -> enum을 사용하기때문에 주석처리하였음
 - insert시에 null인 필드를 제거해줌
 - role을 null로 안넣고 default값 넣어주려고 사용

 #### ✔  @Enumerated 어노테이션
  - DB는 RoleType이 없어서 알려줘야댐
  - EnumType을 사용할꺼고 타입은 String이다.