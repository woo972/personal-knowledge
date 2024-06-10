---
tags:
  - dev
  - java
  - async
  - thread
  - concurrency
dg-publish: true
---
- common pool instance를 반환하는 메서드이다. 프로그램이 종료되기 전에 완료되어야 하는 모든 비동기 task는 commonPool() 메서드를 호출해야 한다. ForkJoinPool.shutdown(), ForkJoinPool.shutdownNow()를 호출해도 실행중인 상태에는 영향을 미치지 않는다.
- commonPool.getParallelism()를 호출하면 가용한 스레드 수를 받아올 수 있다.