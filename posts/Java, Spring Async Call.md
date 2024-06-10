---
tags:
  - dev
  - java
  - async
  - thread
  - spring
dg-publish: true
---
## 방법
---
### ExecutorService
### @Async (Spring)
### Appendix
---
- `java: local variables referenced from a lambda expression must be final or effectively final` : 람다 표현식에서 사용하는 지역변수가 명시적으로 final이거나 사실상 final과 동일한 변수여야 한다. 람다에서 외부 지역변수를 참조할 때 런타임 문제를 방지하기 위해 해당 변수가 변경되지 않는다는 보장이 필요하다