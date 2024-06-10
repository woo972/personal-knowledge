---
tags:
  - dev
  - fault_tolarence
  - incident
dg-publish: true
---
## 개요
---
tbd
## 구현
---
tbd
## 관련 설정 값
---
- max concurrent calls = 256 : 벌크헤드가 서포트 가능한 동시 요청 수
- max wait duration = Duration.ZERO : 벌크헤드가 채워진 이후 다시 가능해졌을 때 요청이 벌크헤드를 타기 위해 대기하는 시간
- fair call handling enabled = false : 세마포어의 FairSync / NonFairSync 중 어느 것을 선택할지 결정 (** FairSync: 요청이 내부 큐에 의해 FIFO로 처리)