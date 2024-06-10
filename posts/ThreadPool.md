---
tags:
  - dev
  - java
  - thread
  - concurrency
dg-publish: true
---
## 개요
---
java.util.concurrent에서 구현된 대부분의 executor는 worker thread로 구성된 thread pool을 사용한다. thread의 생성, 할당 등의 관리 작업은 많은 오버헤드를 발생 시키므로 제한된 pool 내에서 활용하는 것이 바람직하다. 대표적으로 fixed thread pool이 있으며, 장점으로는 항상 고정된 수의 thread만 제공함으로써 시스템의 리소스 사용을 적절하게 제어할 수 있다는 것이다.(웹 어플리케이션에서 HTTP 요청마다 thread를 생성한다고 할 때, 매번 새로운 thread를 만들면 서버에 과부하가 발생하므로, 처리 가능한 요청만을 다루게 할 수 있다)

간단하게 thread pool을 사용하는 executor를 만드는 방법으로는 [[Executors]]의 팩토리 메서드인 [[newFixedThreadPool]](fixed thread pool 생성), `newSingleThreadPool`(한번에 한 task만 수행하는 executor 생성) 등 을 호출하는 것이다.  

만일 이러한 팩토리 메서드가 적합하지 않다면, `java.util.concurrent.ThreadPoolExecutor`와 같은 다른 선택지도 있다.
## 참조
---
- [javadoc: ThreadPoolExecutor](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ThreadPoolExecutor.html)
- [How to configure ThreadPool size](https://netflixtechblog.com/fault-tolerance-in-a-high-volume-distributed-system-91ab4faae74a)