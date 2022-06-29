## ch38_회원가입하기 Ajax요청
### 2022.06.23

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
		// ajax호출시 default가 비동기 호출
		// ajax통신을 이용해서 3개의 데이터를 json으로 변경하여 insert요청
		$.ajax({
			// 회원가입 수행 요청
			type : "POST",
			url:"/blog/api/user",
			data:JSON.stringify(data), // java객체를 json형태로 변경
			contentType:"application/json; charset=utf-8", // body데이터가 어떤 타입인지
			dataType:"json" // 요청을 서버로해서 응답이 왔을 때 생긴게 json이라면(기본적으로 모든것이 문자열) ->
							// JS오브젝트로 변경
		}).done(function(resp){
			// 요청이 성공하면 ㄱㄱ
			alert("회원가입이 완료되었습니다.")
			alert(resp)
			location.href="/blog";
		}).fail(function(error){
			// 요청이 실패하면 ㄱㄱ
			alert(JSON.stringify(error));
		});
	}
}

index.init();
```

#### ✔ $.ajax - done - fail
 - ajax요청하기
 - 성공적으로 끝나면 done에있는 함수 실행
 - 실패하면 fail에 있는 함수 실행

> **ResponseDto**
```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class ResponseDto<T> {
	HttpStatus status;
	T data;
}
```
#### ✔ ResponseEntity<T> 대신 객체를 만들어서 사용