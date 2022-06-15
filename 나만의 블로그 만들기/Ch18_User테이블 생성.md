## OwnMate - 운동 메이트 추천 사이트
### 05.18
#### 1. 좋아요, 싫어요 버튼 기능 구현 고민...
#### 2. 회원가입 id 중복체크 어떻게 할래?
 
### 05.19
#### 1. 회원가입 시 파일 업로드 문제 해결해야댐..
#### 2. 로그인, JWT 구현해야댐...




### 개발 중 오류...
#### 1. resultMap 선언 후 resultMap 대신 resultType으로 작성
`Cause: java.lang.ClassNotFoundException: Cannot find class: reviewMap`
 - resultType을 resultMap으로 변경하여 오류 해결
 #### 2. pw를 uuid로 변경해서 넣어주니 데이터 길이 초과
 `Cause: com.mysql.cj.jdbc.exceptions.MysqlDataTruncation: Data truncation:`
 - MySQL에서 pw의 길이를 varchar(30)에서 varchar(100)으로 변경