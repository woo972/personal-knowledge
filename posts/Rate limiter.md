---
tags:
  - dev
  - rate_limiter
  - system_design
  - architecture
---
## 정의
---
(주로 분산) 대규모 시스템에서 서비스의 과도한 부하를 방지하기 위해 인입되는 트래픽을 throttling하는 방법
### 사용처
- 다른 사용자의 요청은 수락하면서 트래픽 spike를 유발하는 특정 사용자를 제한
- 갑작스럽게 대량의 요청을 보내는 등 서비스에 악영향을 끼치는 사용자 제한
- 다량의 요청이 유입되는 상황에서 우선순위가 높은 요청은 받고, 낮은 요청은 제한
## 구현
---
### 알고리즘 
- Token bucket
- Fixed window counter
- Sliding window counter
- ...
### 
## 참고
---
[woo972/simple_rate_limiter: rate limiter practice (github.com)](https://github.com/woo972/simple_rate_limiter)