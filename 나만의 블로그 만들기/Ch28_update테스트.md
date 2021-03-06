## ch28_update테스트
### 2022.06.23

#### Update 1번 방법 - userRepositoy.save 활용
> **DummyControllerTest**
```java
	//업데이트
	@PutMapping("/dummy/user/{id}")
	public User updateUser(@PathVariable int id,@RequestBody User requestUser) {
		System.out.println("id : " + id);
		System.out.println("password : " + requestUser.getPassword());
		System.out.println("email : " + requestUser.getPassword());
		
		User originUser = userRepositoy.findById(id).orElseThrow(()->{
			return new IllegalArgumentException("수정에 실패하였습니다.");
		});
		originUser.setPassword(requestUser.getPassword());
		originUser.setEmail(requestUser.getEmail());
		userRepositoy.save(originUser);
		return null;
	}
```

#### ✔ Step
 - userRepositoy.findById를 통해 해당 Id의 originUser를 찾아온다.
 - originUser에 새로 입력받은 값들을 최신화 해준다.
 - userRepositoy.save(originUser)로 DB에 저장한다.


#### Update 2번 방법 - @Transactional 활용
> **DummyControllerTest**
```java
	//업데이트
	@Transactional //함수 종료시에 자동 commit이 됨.
	@PutMapping("/dummy/user/{id}")
	public User updateUser(@PathVariable int id,@RequestBody User requestUser) {
		System.out.println("id : " + id);
		System.out.println("password : " + requestUser.getPassword());
		System.out.println("email : " + requestUser.getPassword());
		
		User originUser = userRepositoy.findById(id).orElseThrow(()->{
			return new IllegalArgumentException("수정에 실패하였습니다.");
		});
		originUser.setPassword(requestUser.getPassword());
		originUser.setEmail(requestUser.getEmail());
		~~~userRepositoy.save(originUser);~~~
		return null;
	}
```
#### ✔ Step
 - userRepositoy.findById를 통해 해당 Id의 originUser를 찾아온다.
 - originUser에 새로 입력받은 값들을 최신화 해준다.
 - @Transactional 태그를 붙혀준다.

#### ✔ @RequestBody
 - Json형태의 데이터를 받기 위해 사용한다.

 #### ✔ @Transactional
 - 함수가 호출될때 실행되었다가 함수가 종료되면 Transacti이 끝남
 - 함수가 종료되면 자동 commit된다.
 - commit이 되면서 값이 변경되었기 때문에 자동으로 flush한다. = 더티체킹!!