## ch63_카카오 로그인 OAuth2.0 개념 이해
### 2022.07.13

#### ✔ 카카오 로그인만 유지했을 때 문제점
####% 쇼핑몰의 경우?
 - 고객의 주소를 유지해야하는데 카카오 로그인으로는 알 수 없다.
 - 고객의 등급을 주문 가격에 대해서 차등으로 부여할 수 없다.
 - 따라서 웹 페이지만의 독자적인 회원가입과 카카로 로그인을 연동해야한다.
 👉 평소 사용하는 사이트의 SNS 연동하기를 생각하면 될 듯!!

#### ✔ OAuth 2.0?
 - Open Auth : 인증처리를 대신 해준다.
##### 일반적인 페이지
 <img src="https://user-images.githubusercontent.com/97611103/178741047-7222b7c2-f685-4417-b70d-f97deacf53f7.png" height="400px" width="300px"></img>

##### OAuth를 사용한 페이지
 - 









### Session값 변경하기

![image](https://user-images.githubusercontent.com/97611103/178022334-5da9b374-9df2-4c93-aac7-6d8908ea2c0e.png)
 #### Session 생성과정
 - SecurityContextHolder -> SecurityContext -> Authentication안에 세션의 값이 저장이된다.
 	- 로그인 요청이오면 AuthenticationFilter 작동 -> Filter에서 Username, Password로 토큰 생성
 	- 이 토큰으로 AuthenticationManager가 Authentication 객체를 만든다. But. 객체를 만들기 위해서는 조건이 필요함.
 		- Username을 UserDetailsService에 던져서 DB에 해당 User가 있는지 확인.
		- 있으면 해당 User를 Manager에 다시 던져준다.
		- Manager는 토큰의 password를 Bcrpyt로 암호화하고 돌려받은 User의 비밀번호와 비교한다.
		- 비밀번호가 일치하면 객체를 생성하고 시큐리티 컨텍스트에 저장한다!!
- 따라서 Session값을 변경하고싶으면 Authentication객체를 강제로 만들어서 Session에 넣어주면 된다.
 
> SecurityConfig.java
```java
	@Bean
	@Override
	public AuthenticationManager authenticationManagerBean() throws Exception {
		// TODO Auto-generated method stub
		return super.authenticationManagerBean();
	}
```
#### ✔ authenticationManager를 만들기위해서 추가해준다.

> userService.java
```java
	//변경된 계정으로 세션 새로 등록
	Authentication authentication = authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(user.getUsername(),user.getPassword()));
	SecurityContextHolder.getContext().setAuthentication(authentication);
```
#### ✔ authenticationManager에게 새로운 username과 pw를 주고 authentication객체를 만들도록 시킨다.

#### ✔참고
- 유튜브 강의 : https://www.youtube.com/watch?v=JBN5dCnLYnY&list=PL93mKxaRDidECgjOBjPgI3Dyo8ka6Ilqm&index=65
