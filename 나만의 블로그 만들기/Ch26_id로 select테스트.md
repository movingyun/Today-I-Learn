## ch26_id로 select테스트
### 2022.06.22

> **DummyControllerTest**
```java
	//{id} 주소로 파라미터를 전달 받을 수 있음.
	//http://localhost:8000/blog/dummy/user/3
	@GetMapping("/dummy/user/{id}")
	public User detail(@PathVariable int id) {
		//id로 조회를 하자.
		//있으면 userRepositoy.findById(id)로 찾아오고
		//없으면 override된 함수로 해당유저 없다고 메세지 날려주자
		User user = userRepositoy.findById(id).orElseThrow(new Supplier<IllegalArgumentException>() {
			@Override
			public IllegalArgumentException get() {
				// TODO Auto-generated method stub
				return new IllegalArgumentException(id+"번 유저는 없습니다.");
			}
		});
		return user;
	}
```
#### ✔ @PathVariable
 - Get방식에서 URL경로에 있는 값을 파라미터로 추출.

#### ✔ orElseThrow
 - 정확하지 않은 값이 파라미터로 들어왔을 때 예외처리를 해준다.
 ![image](https://user-images.githubusercontent.com/97611103/174955441-ab92c830-e4d3-43c4-9ca5-735f99b4689f.png)
 - 후에 AOP를 활용해서 처리해준다.
 
#### ✔ 자바 오브젝트 -> JSON타입 변환
 - 웹 브라우저에서 object타입의 user를 인식할 수 없다. 따라서 변환 해줘야 한다.
 - 기존엔 Gson 라이브러리를 사용했다.
 - 스프링부트에서는 MessageConverter라는 애가 응답시에 자동 작동한다.
 - 만약 자바 object를 리턴하게되면 MessageConverter가 Jackson 라이브러리를 호출해서 user 오브젝트를 json으로 변경한다.