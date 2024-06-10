---
tags:
  - java
  - dev
  - concurrency
  - thread
dg-publish: true
---
## 개요
---
Thread 객체를 통해 thread를 직접 컨트롤하는 것은 효율적이지 못하기 때문에 더 high level에서 동시성을 달성할 수 있도록 하는 것이 필요하다. 특히 thread의 생성과 관리는 어플리케이션의 다른 부분과 분리되는 것이 필요하다. 

Executors는 다음과 같은 3가지 타입의 인터페이스를 포함해 몇 가지 인터페이스를 위한 팩토리 및 유틸 메서드를 가지고 있다.
- `Executor`: 새로운 task를 실행시키는 인터페이스
- `ExecutorService`: `Executor` 자체나 다른 개별 태스크의 라이프사이클을 매니징하는 `Executor`의 서브 인터페이스
- `ScheduledExecutorService`: 미래 혹은 정기적 task의 수행을 다룰 수 있는 `ExecutorService`의 서브 인터페이스
## Executor
---
execute() 메서드 하나만을 갖고 있는 인터페이스로, 기존의 thread 생성을 대체할 수 있다. Thread.start() 사용시 thread를 새로 생성하고 바로 실행시키는 데 반해 Executor.execute()를 사용하면 [[ThreadPool]]을 이용하여 인자로 받은 Rannable을 기존에 존재하는 worker thread로 실행시키거나 worker thread 사용이 가능해질 때까지 queue에 넣고 대기시킨다.
```java

Runnable r = () -> { ... };

// Thread 사용
Thread t = new Thread(r);
t.start();

// Executor 사용
Executor e = (Excecutor 생성)
e.execute(r);
```
## ExecutorService
---
Executor.execute()를 대체하는 submit() 메서드를 가지고 있다. 이 메서드는 Runnable과 Callable을 모두 인자로 받을 수 있다. submit()은 리턴값으로 Future 객체를 받는데, Callable의 리턴값을 가져오거나 Runnable과 Callable의 상태를 관리할 수 있다. 

또한 shutdown() 등 몇가지의 메서드가 있어서 executor의 종료를 관리할 수 있는데, task들은 이러한 interrupt를 적절히 처리해야한다.
## ScheduledExecutorService
---
ExecutorService의 기능들을 shcedule로 보강하여 Runnable 혹은 Callable을 특정한 딜레이와 함께 수행할 수 있다. 또한 `scheduleAtFixedRate`와 `scheduleWithFixedDelay`를 정의하고 있어서 특정한 task들을 정의된 interval에 따라 수행하는 것도 가능하다.
## 참조
---
- [[Thread]]
- [[ThreadPool]]




