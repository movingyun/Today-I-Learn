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

#### ✔ @ControllerAdvice
 - 어디서든 예외가 발생하면 여기서 처리한다.

#### ✔ @ExceptionHandler
 - 처리하고싶은 예외를 지정해 준다.
 - value = "내가 처리 할 예외"

 