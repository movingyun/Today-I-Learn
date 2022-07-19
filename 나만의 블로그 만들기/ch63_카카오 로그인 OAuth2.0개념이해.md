## ch63_카카오 로그인 OAuth2.0 개념 이해
### 2022.07.13

#### ✔ 카카오 로그인만 유지했을 때 문제점
#### 쇼핑몰의 경우?
 - 고객의 주소를 유지해야하는데 카카오 로그인으로는 알 수 없다.
 - 고객의 등급을 주문 가격에 대해서 차등으로 부여할 수 없다.
 - 따라서 웹 페이지만의 독자적인 회원가입과 카카로 로그인을 연동해야한다.
 👉 평소 사용하는 사이트의 SNS 연동하기를 생각하면 될 듯!!

#### ✔ OAuth 2.0?
 - Open Auth : 인증처리를 대신 해준다.
##### 일반적인 페이지
 <img src="https://user-images.githubusercontent.com/97611103/178741047-7222b7c2-f685-4417-b70d-f97deacf53f7.png" height="200px" width="300px"></img>

##### OAuth를 사용한 페이지
 <img src="https://user-images.githubusercontent.com/97611103/179752239-9348f412-3ba5-4a82-bde0-96470672d696.png
" height="350px" width="600px"></img>
 - 홍길동이 블로그서버한테 카카오 서버에 접근할 수 있는 권한을 위임한 것.
 - OAuth 로그인의 2가지 절차
	- 인증하기 : code
	- 권한 부여 : AccessToken
 - OAuth2 client라이브러리를 사용하면 구글, 페이스북 로그인 쉽게 만들 수 있음.

#### ✔참고
- 유튜브 강의 : https://www.youtube.com/watch?v=JBN5dCnLYnY&list=PL93mKxaRDidECgjOBjPgI3Dyo8ka6Ilqm&index=65
