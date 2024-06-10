---
tags:
  - dev
  - java
  - exception
dg-publish: true
---
## Checked Exception
---
checked exception은 컴파일 타임에 확인된다. 즉, 명시적으로 exception 핸들링을 위한 처리를 해주어야 한다. (메서드 선언시 throws xxxException 등을 붙여주거나 try-catch 블록으로 처리)

Exception 하위 클래스 중 RuntimeException을 제외한 예외(IOException 등)가 checked exception에 해당한다. 일반적으로 외부 리소스와의 상호작용이나 네트워크 통신 등 예측가능한 예외 상황에서 사용된다.
```java
public void test(){
	try{
		throw new IOException("checked exception");
	}catch(IOException e){
		... doSomething ...
	}
}
```
## Unchecked Exception
---
unchecked exception은 런타임에 확인된다. 즉 컴파일러가 예외를 확인하지 않으므로, 코드상에서 명시적으로 핸들링하는 것은 프로그래머의 재량에 달려있다.

RuntimeException을 상속하고 예외(NullPointerException, ArrayIndexOutOfBoundsException 등)들이 unchecked exceptiondp 해당된다. 일반적으로 프로그램의 논리오류에 사용된다.
```java
public void test(){
	int result = 10 / 0; // ArithmeticException 발생
}
```