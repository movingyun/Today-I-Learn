## ch51_XSS와 CSRF
### 2022.07.04

#### XSS(Cross-Site Scripting)란?
 - 악의적인 사용자가 공격하려는 사이트에 스크립트를 넣는 기법이다.
 - 주로 다른 웹사이트와 정보를 교환하는 식으로 작동하므로 사이트 간 스크립팅이라고 명칭한다.
 - 공격 방법에 따라 Stored XSS와 Reflected XSS로 나뉜다.
![image](https://user-images.githubusercontent.com/97611103/177112336-cf0a4755-bdc0-49d3-9f89-c352124c707c.png)

#### CSFR(Cross-Site Request Fogery)란?
 - 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격이다. 
 - 사용자가 웹사이트에 로그인한 상태에서 사이트간 요청 위조 공격 코드가 삽입된 페이지를 열면, 공격 대상이 되는 웹사이트는 위조된 공격 명령이 믿을 수 있는 사용자로부터 발송된 것으로 판단하게 되어 공격에 노출된다.
 - 위조 요청을 전송하는 서비스(ex : 페이스북)에 희생자가 로그인 상태여야한다.
 - ex) 네이버 포인트 올리기(Admin권한을 가진 희생자가 잘못된 링크를 클릭함으로써 user의 포인트를 올려준다.)


#### XSS와 CSRF의 차이점
![image](https://user-images.githubusercontent.com/97611103/177112409-b6a89402-bae3-4520-a920-31096ffff83a.png)

#### 방지대책
![image](https://user-images.githubusercontent.com/97611103/177112562-215cf414-89ed-4dab-92af-a826a26a7bd3.png)


#### ✔참고
- https://www.youtube.com/watch?v=cC1tI8cOOOk&list=PL93mKxaRDidECgjOBjPgI3Dyo8ka6Ilqm&index=53
- https://lucete1230-cyberpolice.tistory.com/23



