---
tags:
  - dev
  - java
  - async
---
- 비동기 작업의 결과를 나타내는 클래스로 [[Future]] 인터페이스를 구현하고 있다.
- java.util.concurrent 패키지 소속이다.
- 주어진 Supplier를 호출하여 값을 받아온뒤 new CompletableFuture를 반환한다. [[ForkJoinPool.commonPool()]]에서 수행되는 task에 의해 수행된다
```
Future<Integer> future = CompletableFuture.supplyAsync(()-> doSomethingHasReturn())
```
```
CompletableFuture.runAsync(()-> doSomething)
```

- 예시 코드 
	- main 메서드에서 실행할 Test.parent() 메서드는 `[parent]main` 을 출력한다.
	- 별도 스레드에서 실행할  Test.child() 메서드는 `[child]ForkJoinPool.commonPool-worker-<n>`을 출력한다. (비동기이기 때문에 `<n>` 숫자는 변할 수 있음)
```java
public class Test {  
    public void parent(){  
        System.out.println("[parent]"+Thread.currentThread().getName());  
        CompletableFuture.runAsync(() -> child());  
        CompletableFuture.runAsync(() -> child());  
    }  
  
    private void child() {  
        System.out.println("[child]"+Thread.currentThread().getName());  
    }  
}
```
