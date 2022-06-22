## ch24_회원가입을 위한 insert테스트
### 2022.06.22

> **DummyControllerTest**
```java
package com.cos.blog.test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RestController;

import com.cos.blog.model.User;
import com.cos.blog.repositoy.UserRepository;

@RestController
public class DummyControllerTest {
	
	@Autowired //의존성 주입(DI)
	private UserRepository userRepositoy;
	
	// http://localhost:8000/blog/dummy/join(요청)
	// http의 body에 username, password, email 데이터를 가지고(요청)
	@PostMapping("/dummy/join")
	public String join(User user) { //입력값을 Object(user)로 받을 수 있음
		System.out.println("username : " + user.getUsername() );
		System.out.println("password : " + user.getPassword() );
		System.out.println("email : " + user.getEmail() );
		
		userRepositoy.save(user);
		
		return "회원가입이 완료되었습니다.";
	}
}
```
#### ✔  파라미터를 Object(user)로 받을 수 있음
 - String username, String password, String email 처럼 값을 하나씩 주지 않아도 Object로 한번에 받아올 수 있다.


#### ✔ Talend 이용시 주의사항
 - 입력 형식을 Form(or x-www-form-urlencoded)로 해주어야 key-value형태로 값을 요청한다.
 - ex) key=value&key=value

![Talend이미지](https://user-images.githubusercontent.com/97611103/174937992-b1dd57b5-bf01-4878-9dfa-94a08034c340.png)