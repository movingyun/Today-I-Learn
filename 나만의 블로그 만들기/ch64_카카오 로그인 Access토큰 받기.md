## ch64_카카오 로그인 Access토큰 받기
### 2022.07.19

### 카카오 로그인 버튼 만들기
```
<a href="#">
   <img height="38px" src="/image/kakao_login_button.png">
</a>
```

### 카카오 로그인 요청 주소 가져오기
> https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api에서 가져올 수 있음.
 - https:/kauth.kakao.com/oauth/authorize?client_id=클라이언트키&redirect_uri=로그인요청콜백주소&response_type=code

### 로그인 창 띄우기 성공
 - 동의하고 계속하기 누르면 아래와 같은 페이지 뜬다.
 <img src="https://user-images.githubusercontent.com/97611103/179757679-2abb8487-3f8b-4d3d-98cc-540e6e62df3c.png" height="200px" width="800px"></img>
 - 요청 url확인해보면 ~~~~code=F_-AibHXU-tv32W7OWU9dt4D5BlEYzqsuPnUbcu7O5oAkZurvucmi0biOWGLBg9DRdoZcQopyNkAAAGCFpJT0Q라고 나와있음.
 - 이 요청에대한 컨트롤러 작성해주면 된다.

### 요청 받는 컨트롤러 만들기
```java
@GetMapping("/auth/kakao/callback")
public @ResponseBody String kakaoCallback(String code) {
	return "카카오 인증 완료"+code;
}
```
 <img src="https://user-images.githubusercontent.com/97611103/179758909-cffbb716-1712-4071-b069-670285c8b589.png
" height="100px" width="800px"></img>
 - 인증이 잘 된것 확인.
 - 인증된 코드를 통해 AccessToken을 받아보자.

### 사용자 토큰 받기
> 인가 코드로 토큰 발급을 요청합니다. 인가 코드 받기만으로는 카카오 로그인이 완료되지 않으며, 토큰 받기까지 마쳐야 카카오 로그인을 정상적으로 완료할 수 있습니다. 필수 파라미터를 포함하여 POST로 요청합니다. 요청 성공 시 액세스 토큰, 리프레시 토큰과 토큰 정보를 포함한 JSON 객체를 받습니다. OpenID Connect를 사용하는 앱인 경우, 응답에 ID 토큰이 함께 포함됩니다.

<img src="https://user-images.githubusercontent.com/97611103/179759732-b013ef79-b30b-4d2f-aa7d-b748817c8613.png
" height="500px" width="800px"></img>
 - Content-type형태로 아래 5가지 데이터를 http body에 전달
 - grant_type=authorization_code
 - client_id=e99501c29dc96fc3dd715b383757d655
 - redirect_uri= http://localhost:8000/auth/kakao/callback
 - code = 동적임.
 - client_secret : 필수는 아니다

```java
@GetMapping("/auth/kakao/callback")
public @ResponseBody String kakaoCallback(String code) {
	
	//POST방식으로 key=value데이터를 요청(카카오쪽으로)
	//POST방식으로 데이터를 보내려면 RestTemplate라는 라이브러리 사용
	//Retrofit2(안드로이드에서 사용), OkHttp(예전에 사용)
	
	RestTemplate rt = new RestTemplate();
	
	//Http 오브젝트 생성
	HttpHeaders headers = new HttpHeaders();
	headers.add("Content-type", "application/x-www-form-urlencoded;charset=utf-8");
	
	//Http Body 오브젝트 생성(바디에 담아서 날릴거 작성)
	MultiValueMap<String, String> params = new LinkedMultiValueMap<>();
	params.add("grant_type", "authorization_code");
	params.add("client_id", "e99501c29dc96fc3dd715b383757d655");
	params.add("redirect_uri", "http://localhost:8000/auth/kakao/callback");
	params.add("code", code);
	
	//HttpHeader와 HttpBody를 하나의 오브젝트에 담기(아래서 한번에 보내야 함)
	HttpEntity<MultiValueMap<String, String>> kakaoTokenRequest =
			new HttpEntity<>(params, headers);
	
	//Http요청하기 - Post방식으로 - 그리고 response변수의 응답 받음
	ResponseEntity<String> response = rt.exchange(
			"https://kauth.kakao.com/oauth/token", //보내는 주소
			HttpMethod.POST, //보내는 형식
			kakaoTokenRequest, //http body, http header
			String.class //응답을 받을 타입
			);
	
	return "카카오 토큰 요청 완료"+response;
}
```
<img src="https://user-images.githubusercontent.com/97611103/179763724-0be23414-f14a-4bca-9bf2-7e59a541987c.png" height="200px" width="800px"></img>
 - 200을 보니 요청이 정상적으로 보내졌음.
 - 받은 access_token으로 카카오 서버에서 유저의 정보를 꺼내볼 수 있음.

#### ✔참고
- 유튜브 강의 : https://www.youtube.com/watch?v=NwQ_55l0Za4&list=PL93mKxaRDidECgjOBjPgI3Dyo8ka6Ilqm&index=66