---
tags:
  - dev
  - java
  - thread
  - concurrency
  - async
---
daemon thread는 주로 프로그램의 보조적인 성격으로 백그라운드에서 수행되는 thread로, 프로그램 종료시 다른 thread의 종료를 기다리는 반면, daemon thread의 종료여부는 중요하지 않다. 예로, Garbage Collector는 deamon thread로 실행된다. 프로그램을 종료하면 GC를 수행할 필요가 없다.