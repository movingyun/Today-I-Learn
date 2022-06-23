## ch31_Exception처리하기
### 2022.06.23

> **GlobalExceptionHandler**
```java
package com.cos.blog.handler;

import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;
import org.springframework.web.bind.annotation.RestController;

@ControllerAdvice //모든 exception이 생기면 일로들어와
@RestController
public class GlobalExceptionHandler {
	
	@ExceptionHandler(value = IllegalArgumentException.class)
	public String handleArgumentExeption(IllegalArgumentException e) {
		return "<h1>"+e.getMessage() +"</h1>";
	}
}

```
![예외처리 전](https://user-images.githubusercontent.com/97611103/175309960-3ece4942-6564-45a6-b613-349c6a25c164.png)
![예외처리 후](https://user-images.githubusercontent.com/97611103/175309805-12915bec-e451-4588-836f-9bc35099334c.png)

#### ✔ @ControllerAdvice
 - 어디서든 예외가 발생하면 여기서 처리한다.

#### ✔ @ExceptionHandler
 - 처리하고싶은 예외를 지정해 준다.
 - value = "내가 처리 할 예외"

 