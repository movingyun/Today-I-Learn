## ch21_Reply테이블 생성
### 2022.06.15

> **DTO - Reply**
```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder //빌더패턴
@Entity
public class Reply {
	@Id//primary key 주기
	@GeneratedValue(strategy = GenerationType.IDENTITY) //프로젝트에서 연결된 DB의 넘버링 전략을 따라감.(=mySQL에서는 auto_increment를 사용하겠다!)
	private int id; //auto_increment
	
	@Column(nullable = false,length = 200)
	private String content; //섬머노트 라이브러리 사용 - <html>태그가 섞여서 디자인됨
	
	@ManyToOne
	@JoinColumn(name="boardId")
	private Board board;
	
	@ManyToOne //한명의 user가 여러 reply를 달수있다.
	@JoinColumn(name="userId")
	private User user;
	
	@CreationTimestamp
	private Timestamp createDate;
}
```
 #### ✔ ManyToOne인지 ManyToMany인지 확실하게 확인하자!!