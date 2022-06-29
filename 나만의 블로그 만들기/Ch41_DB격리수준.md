## ch41_DB격리수준
### 2022.06.29

#### ✔ 트랜잭션 : 일이 처리되기 위한 가장 작은 단위
 - 여러 트랜잭션이 모여 하나의 트랜잭션이 될 수 있고 이런것을 **서비스**라고 부른다!!

#### ✔ 트랜잭션 격리수준 : 고립도와 성능의 Trade-off를 조절한다.
 - READ UNCOMMITTED : 다른 트랜잭션에서 커밋되지 않은 내용도 참조할 수 있다
	![image](https://user-images.githubusercontent.com/97611103/176362412-8c01f8e7-af1d-49e0-a6f7-abc8b3e4518f.png)
	##### 특징
	```
	Dirty Read, Non-Repeatable Read, Phantom Read 현상이 발생한다.
	```
	
	##### 문제점
	```
	데이터 정합성에 문제가 많다. 그렇기에 RDBMS 표준에서는 격리수준으로 인정하지 않는다.
	```
 - READ COMMITTED : 다른 트랜잭션에서 커밋된 내용만 참조할 수 있다.
 	![image](https://user-images.githubusercontent.com/97611103/176362567-f77d5bc4-aa47-4966-80a3-ca50d63de2ae.png)

	##### 특징
	```
	Dirty Read 가 발생하지 않지만 (트랜잭션이 COMMIT되어 확정된 데이터만 읽는 것을 허용)
	Non-Repeatable Read, Phantom Read 현상은 여전히 발생한다.
	```
	##### 문제점
	```
	NON-REPEATABLE READ 부정합 문제가 발생할 수 있다.
	```
 - REPETABLE READ : 트랜잭션에 진입하기 이전에 커밋된 내용만 참조할 수 있다.
	![image](https://user-images.githubusercontent.com/97611103/176362754-1cbc271f-33e9-45b5-8fab-525e43cb050e.png)
	##### 특징
	```
	변경되기 전 레코드는 Undo 공간에 백업해두고 실제 레코드 값을 변경한다.
	Dirty Read와 같은 현상은 발생하지 않지만 Phantom Read 현상은 여전히 발생한다.
	```
	##### 문제점
	```
	하나의 트랜잭션 실행시간이 길어질수록 Undo에 백업된 레코드가 많아져서 멀티 버전을 관리해야하는 단점이 있다.
	(하지만 영향을 미칠정도로 트랜잭션이 오래 지속되는 경우가 없어서 READ COMMITTED와 REPEATABLE READ의 성능 차이는 거의 없다고 한다.)
	또한 UPDATE 부정합와 Phantom Read가 발생할 수 있다.
	```
 - SERIALIZABLE : 트랜잭션에 진입하면 락을 걸어 다른 트랜잭션이 접근하지 못하게 한다.
	##### 특징
	```
	가장 단순한 격리 수준이지만 가장 엄격한 격리 수준으로 Phantom Read가 발생하지 않는다.
	```
	##### 문제점
	```
	동시 처리 능력이 다른 격리수준보다 떨어지고 성능저하가 발생하여 데이터베이스에서 거의 사용되지 않는다.
	```

#### ✔ 트랜잭션 격리 수준이 필요한 이유?
 - 일관성(Consistency)을 지키기 위해서.


#### ✔ 참고
 - https://velog.io/@guswns3371/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B2%A9%EB%A6%AC%EC%88%98%EC%A4%80
