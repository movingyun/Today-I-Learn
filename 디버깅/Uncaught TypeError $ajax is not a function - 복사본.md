## Refused to execute script from 'http://localhost:8000/auth/loginForm' because its MIME type ('text/html') is not executable, and strict MIME type checking is enabled.
### 2022.07.4

#### SecrutiyConfig.java
```java
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
			.authorizeRequests() //request가 들어오면
				.antMatchers("/auth/**") 
				.permitAll()
				.anyRequest() //이거 빼고는
				.authenticated() //다 인증이 되어야 함.
			.and()
				.formLogin()
				.loginPage("/auth/loginForm");
	}
```
> antMatchers("/auth/**")를 사용해 auth가 붙은 경로는 로그인을 하지 않아도 갈수있게 했음

#### joinForm.jsp
```jsp
<form action="/user/join" method="POST">
...
<script src="/js/user.js"></script>
```
> 하지만 버튼이 눌리면 js가 반응해야된다.

#### SecrutiyConfig.java
```java
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
			.authorizeRequests() //request가 들어오면
				.antMatchers("/auth/**","/js/**","/css/**","/image/**")
				.permitAll()
				.anyRequest() //이거 빼고는
				.authenticated() //다 인증이 되어야 함.
			.and()
				.formLogin()
				.loginPage("/auth/loginForm");
	}
```
> 로그인 하지 않아도 갈 수 있는 경로("/js/**" 등) 추가