## ch20_Board테이블 생성
### 2022.06.15

> **DTO - Board**
```java
@Entity //Board클래스가 MySQL에 자동으로 테이블이 생성이 된다.
public class Board {
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY) //auto_increment
	private int id;
	
	@Column(nullable = false, length = 100)
	private String title;
	
	@Lob //대용량 데이터 쓸 때 사용
	private String content; //섬머노트 라이브러리 사용 - <html>태그가 섞여서 디자인됨
	
	@ColumnDefault("0")
	private int count; //조회수
	
	@ManyToOne //객체관계 생성 //Many = Board, User = One -> 한명의 유저는 여러개의 게시물 작성 
	@JoinColumn(name="userId") //userId라는 컬럼으로 만들어
	private User user;
	
	@CreationTimestamp
	private Timestamp createDate;
}
```
 #### ✔ MySQL에서는 오브젝트를 컬럼으로 만들수없어서 FK를 사용하지만 자바는 오브젝트를 저장할 수 있다.
  - JoinColumn 어노테이션을 활용해서 Join / name속성으로 컬럼 이름 지정
  - ManyToOne 어노테이션으로 객체 관계 설정