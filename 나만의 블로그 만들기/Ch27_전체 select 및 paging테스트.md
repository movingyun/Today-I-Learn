## ch27_전체 select 및 paging 테스트
### 2022.06.22

> **DummyControllerTest**
> 전체 user갖고오기
```java
	@GetMapping("/dummy/user")
	public List<User> list(){
		return userRepositoy.findAll();
	}
```

> User 페이지네이션
```java
	//한페이지당 2건의 데이터를 리턴
	@GetMapping("/dummy/user")
	public List<User> pageList(@PageableDefault(size = 2,sort = "id",direction = org.springframework.data.domain.Sort.Direction.DESC) Pageable pageable){
		Page<User> pagingUser = userRepositoy.findAll(pageable);
		
		List<User> users = pagingUser.getContent();
		return users;
	}
```

#### ✔ 데이터 페이지네이션(@PageableDefault 활용)
 - size = 한 페이지에 들어갈 데이터 수
 - sort = 정렬기준
 - userRepositoy.findAll(pageable)의 반환값이 page여서 .getContent()를 활용해서 그 페이지의 Content만 추출