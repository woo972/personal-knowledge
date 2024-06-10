---
tags:
  - dev
  - java
  - concurrency
  - thread
dg-publish: true
---
멀티 프로세서의 이점을 누리기위한 `ExecutorService` 인터페이스의 특수한 구현 프레임워크이다. 큰 작업을 작은 단위로 recursively하게 쪼개서 thread pool에 존재하는 worker thread에 분산시켜 수행한다. 이를 활용한 작업으로 `Arrays.parallelSort()` 등이 있다. Fork-Join 프레임워크의 핵심은 ForkJoinTask를 수행하기 위해 work-stealing 알고리즘을 구현한 ForkJoinPool에 있다.