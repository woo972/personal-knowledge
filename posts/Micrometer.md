---
tags:
  - dev
  - monitoring
  - metric
dg-publish: true
---
## 개요
---
- Meter Registry(모니터링 시스템)에 측정 데이터를 전달하기 위해 Applicaion에서 실행하는 파사드.
	- meter registry로는 JMX, Graphite, [[Prometheus]] 등이 있다.
- Dimensionality
	- 메트릭 이름에 태그(key-value)를 붙여서 복잡한 정보를 표현할 수 있게 한다(prometheus)
	- 메트릭에 직접 데이터를 push한다(graphite)
- rate aggregation
	- 모니터링 시스템에서 누적된 값을 받아 통계치를 한출한다(prometheus)
	- 어플리케이션에서 통계치를 산출하여 모니터링 시스템에 전달(graphite)
- 
