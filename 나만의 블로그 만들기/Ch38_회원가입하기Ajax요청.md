## ch38_회원가입하기 Ajax요청
### 2022.06.23






> **joinForm.jsp**
```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>

<%@include file="../layout/header.jsp"%>

<div class="container">
	<form action="/user/join" method="POST">
		<div class="form-group">
			<label for="username">Username :</label> <input type="text" class="form-control" placeholder="Enter username" id="username">
		</div>
		<div class="form-group">
			<label for="email">Email :</label> <input type="email" class="form-control" placeholder="Enter email" id="email">
		</div>
		<div class="form-group">
			<label for="password">password :</label> <input type="password" class="form-control" placeholder="Enter password" id="password">
		</div>
	</form>
	<button id="btn-save" class="btn btn-primary">회원가입 완료</button>

</div>
<script src="/blog/js/user.js"></script>
<%@include file="../layout/footer.jsp"%>
```

> **user.js**
```js
let index={
	init: function(){
		$("#btn-save").on("click",()=>{
			this.save();
		});
	},

	save:function(){
		let data = {
			username: $("#username").val(),
			password: $("#password").val(),
			email: $("#email").val()
		}
//		console.log(data);
		$.ajax().done().fail();//ajax통신을 이용해서 3개의 데이터를 json으로 변경하여 insert요청
	}
}

index.init();
```
![image](https://user-images.githubusercontent.com/97611103/175351647-b9c04bbb-c1bc-4b3c-bca9-741fd073c7dc.png)
#### ✔ 파라미터 넘겨주는 방법
 - button에 id(btn-save) 입력
 - js문서를 통해 이벤트 리스너 생성
 - ajax로 넘겨줌.

 #### ✔ 경로를 못찾을 때(user.js경로를 찾기 힘들었다...)
 - console에 오류가 있는지 확인.
 - Network에서 제대로 다운이 됐는지 확인