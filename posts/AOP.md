---
tags:
  - dev
  - aop
  - spring
---
## 개념
---
- Aspect: 모늘화된 관심사 (Advice + PointCut)
- Advice: 구현체 코드
	- 적용될 시점을 어노테이션으로 정의한다 (When)
		- ex) @Before @After @Around 등
- JoinPoint 클라이언트가 호출하는 비즈니스 메서드(point cut의 후보), JoinPoint 인터페이스를 통해 메서드 정보를 획득 가능
	- Signature getSignaturel(): 호출한 메서드의 시그니처(리턴타입, 이름, 매개변수)
	- Object getTarget(): 호출한 메서드를 포함하는 비즈니스 객체
	- Object getArgs(): 호출할 때 넘겨준 매개변수 목록
- PointCut: JoinPoint의 상세스 (Where).
	- ex) ModuleResolverAdapter의 모든 메서드에 때 적용
### @Around
- 메서드 실행 전, 후 모두 컨트롤 가능한 Aspect
- 실행 메서드에서 exception이 발생하더라도 실행된다
- @AfterThrowing으로 exception이 안잡히는 경우도 있는데, 그 경우에도 @Around로는 가능하다