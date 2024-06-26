---
tags: dev,scalability
dg-publish: true
---
## 시스템 확장 및 퍼포먼스 향상 방법
---
- 스케일 업 (Vertical Scaling)
- 스케일아웃 (Horizontal Scaling)
- Load Balancing
- 캐싱(Caching): 일반적이고 고비용의 쿼리는 캐싱하여 db 조회없이 결과를 반환함
- 배치: 실시간으로 쓰기가 필요하지 않은 작업(통계 데이터 등)에 대해서는 배치로 처리 
- 비정규화 및 뷰모델: 조회에 필요한 데이터를 뷰모델로 만들고 DB에도 별도 조인 연산없이 가져오도록 비정규화하여 저장함 (사전에 배치를 통해 DM을 만들거나 nosql 등에 저장해둘 수 있음)
- 비동기 처리: 쓰기 연산을 DB에 바로 적용하지 않고 메시지 브로커를 통해 순차적으로 진행하고, 읽기 연산은 데이터 최신화에 상관없이 진행 (DB부하를 줄일 수 있으나, 동기화되지 않은 데이터를 조회할 수 있음)
- 데이터베이스 다중화(Database Replication): 쓰기 연산은 master db에 하되, 읽기 연산은 load balancing을 통해 여러 db에서 분산하여 수행 함 (쓰기 연산을 여러 db에 동시에 하는 경우 동기화 문제가 생기기 때문에 복잡성이 높아질 수 있음)
- 파티셔닝/샤딩(Database Partitioning)
- DB 트랜잭션 최적화(특히 쓰기): 트랜잭션 범위 튜닝, 동시성 문제를 해결하기 위한 락을 필요시 pessimistic에서 optimistic으로 변경([[DB 동시성 문제-Lock]])