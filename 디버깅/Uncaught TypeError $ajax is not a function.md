## Uncaught TypeError: $.ajax is not a function 오류
### 2022.06.29

```html
<script src="https://code.jquery.com/jquery-3.5.1.slim.js"></script>
}
```
> 용량을 줄이기 위해 slim빌드 jquery를 사용하였는데, 이러면 $.ajax()를 사용할 수 없다.

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

		$.ajax({
			type : "POST",
			url:"/blog/api/user",
			data:JSON.stringify(data), 
			contentType:"application/json; charset=utf-8",
			dataType:"json" 
		}).done(function(resp){
			alert("회원가입이 완료되었습니다.")
			location.href="/blog";
		}).fail(function(error){
			alert(JSON.stringify(error));
		});
	}
}

index.init();
```
> 그래서 slim을 뺀 빌드버전으로 해결한다.
```html
<script src="https://code.jquery.com/jquery-3.5.1.js"></script>
```