---
tags:
  - dev
  - java
  - async
---
## Overview
---
- java.util.concurrent에 소속되어 있다.
- 비동기 연산의 결과를 표현하는 클래스이다.
## Methods
---
- 실행중인 task를 취소하는 메서드. 인자로 true를 넘기면 task interrupt를 시도한다.(모든 task가 interrupt를 처리하도록 구현되어있지 않을 수 있어서 주의필요) false이면 task의 종료를 기다린다.
```
boolean cancel(boolean mayInterruptIfRunning);
```
```
boolean isCancelled();
```
```
boolean isDone();
```
- 계산이 모두 완료될 때까지 기다린 후 결과를 반환한다.
```
V get() throws InterruptedException, ExecutionException;
```
- 타임아웃 세팅을 추가한 get()
```
V get(long timeout, TimeUnit unit)  
    throws InterruptedException, ExecutionException, TimeoutException;
```
## Example
---
```java
public class FutureExample {  
    public void example(){  
        ExecutorService executorService = Executors.newSingleThreadExecutor();  
        Future<String> future = executorService.submit(this::asyncTask);  
        try {  
            System.out.println(future.get());  
        } catch (InterruptedException e) {  
            throw new RuntimeException(e);  
        } catch (ExecutionException e) {  
            throw new RuntimeException(e);  
        }  
    }  
  
    private String asyncTask(){  
        return "hello";  
    }  
}
```