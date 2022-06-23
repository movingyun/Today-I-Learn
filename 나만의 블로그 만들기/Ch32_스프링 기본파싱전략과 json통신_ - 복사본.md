## ch32_스프링 기본 파싱전략과 json통신
### 2022.06.23

#### ✔ Get요청
 - 주소에 데이터를 담아 보낸다.
 - 데이터의 형태는 key=value형식

#### ✔ Post, Put, Delete 요청
 - 데이터를 담아보내야 할 것이 많을 때 사용(ex.로그인, 회원가입 등)
 - Body에 데이터를 담아 보낸다
 - JS로 ajax요청 + 데이터 형태는 json으로 통일한다.

 #### ✔ 스프링 컨트롤러의 파싱 전략
  - 전략 1. key=value데이터를 자동으로 파싱하여 변수에 담아준다.
	```java
	PostMapping("/home")
	public String home(String username, String email){
		return "home";
	}
	```

  - 전략 2. key=value 형태의 데이터를 **오브젝트로** 파싱해서 받아주는 역할도 한다.<br>
    이때 주의 할 점은 **setter**가 없으면 key=value 데이터를 스프링이 파싱해서 넣어주지 못한다.
	```java
	class User {
		private String username;
		private String password;

		public String getUsername(){
			return username;
		}
		public String getPassword(){
			return password;
		}
		public void setUsername(String username){
			this.username = username;
		}
		public void setPassword(String password){
			this.password = password;
		}
	}
	```
	```java
	PostMapping("/home")
	public String home(User user){
		
		return "home";
	}
	```

 #### ✔ key=value가 아닌 데이터는 어떻게 파싱할까?
  - 스프링 컨트롤러에서 json 데이터나 일반 text데이터를 받기 위해서는 @RequestBody 어노테이션이 필요하다.
  	```java
	PostMapping("/home")
	public String home(@RequestBody User user){
		
		return "home";
	}
	```
