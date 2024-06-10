---
tags:
  - dev
  - concurrency
  - thread
---
## 개요
---
정해진 갯수의 thread를 가지는 pool을 생성하여 관리하는 메서드.
정해진 수의 thread가 모두 활성화되어 있으면, 작업을 queue로 보내 대기시키며 해당 queue의 개수는 무한이다.(즉 대기열에 작업이 급속도로 추가되는 작업의 경우 시스템 자원을 급격히 소모할 수 있다) thread가 작업 중간에 exception 등으로 실패할 경우 새로운 thread를 생성하여 대체시킨다. 명시적으로 shutdown 명령을 호출하기 전까지는 thread pool이 계속 존재하게 된다.

- 사용예시
```java
ExecutorService executorService = Executors.newFixedThreadPool(2)
```
## Spring Web에서의 사용
---
web 어플리케이션에서 특정 요청에 대해서 thread pool을 강제하고 싶은 경우, `ExecutorService executorService = Executors.newFixedThreadPool(2)` 와 같이 사용하면 매번 thread pool 할당이 다시 일어나기 때문에 @Bean으로 등록하고 주입받아서 사용하는 것이 좋다. 또한 Spring에서는 ThreadPoolTaskExecutor를 제공해주기 때문에 Spring과의 통합을 위해서는 ThreadPoolTaskExecutor를 사용하는 것이 좋다.
## 참조
---
- https://www.baeldung.com/java-executors-cached-fixed-threadpool
- https://www.baeldung.com/java-rejectedexecutionhandler
