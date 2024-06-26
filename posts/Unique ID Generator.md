---
tags:
  - db
  - system_design
  - dev
dg-publish: true
---
## Context
---
- 분산환경(DB서버가 다수)에서는 DB의 auto_increment를 사용할 경우 DB간 동기화 시 중복 이슈가 있기 때문에 사용이 어렵다
- UUID를 사용하는 경우 데이터가 너무 크기 때문에 성능 및 공간 문제로 사용이 어렵다
## 접근 방법
--- 
### 중앙형 티켓 생성기
- 흐름
	- 다수의 서버에서 Unique ID 생성을 담당하는 티켓 생성기 서비스에 ID를 요청한다
	- 티켓 생성기는 auto increment하는 방식으로 ID를 생성하여 돌려준다
	- 각 서버에서 제공받은 ID로 DB에 저장한다
- 단점
	- 티켓 생성기가 1대이므로 SPoF로 작용한다
	- SPoF를 해결하기 위해 티켓 생성기를 여러대로 확장하는 경우 동기화 문제가 발생한다 (zookeeper 등 사용 필요)
### 트위터 스노우플레이크
- 개념
	- 사인비트 + 타임스탬프 + worker number(데이터센터 ID + 서버 ID) + sequence number(일련번호)로 구성된 64비트 ID를 생성한다
		- 고정 할당: 사인비트, 데이터센터ID, 서버ID는 사전에 정의된 값이다
		- 동적 할당: 타임스탬프, 일련번호
- 용도
	- 사인비트(1bit): 용도 없음, 나중을 위해 설정한다
	- 타임스탬프(41bit): 2^41 - 1 ms -> 약 65년치
		- 2^30 (~= 10^10) x 2^10 (~= 10^3) x 2 = 2000000000000 
		- 2000000000000 / 1000(ms) / 3600(hr) / 24(day) / 365(year) ~= 65 
		- 타임스탬프계산시 현재 기원시각을 제하여 오버플로우를 늦출 수 있다
			- (예) 2000년 1월 1일이 기원시각인경우, 약 900000000000밀리초 이므로 2000000000000 - 900000000000 = 1100000000000 ( 약 69년치 )
			- 기간 도래시 기원시각을 변경하는 작업이 필요하다
		- 혹은 사인비트나 다른 비트를 더 할당하여 기간을 늘릴 수도 있을 것이다
	- 데이터센터(5bit): 2^5 = 32군데 데이터 센터 지원가능
	- 서버(5bit): 2^5 = 32대 서버 지원가능
	- 일련번호(12bit): 동시에 ID생성시 증가 시키며, 밀리초마다 0으로 갱신된다
- 장점
	- 아이디 자체로 시간순서 정렬이 가능하며, 데이터의 선후관계를 알 수 있다
	- 서버가 확장되어도 대응이 가능하다
- 단점
	- 여러 서버에서 실행될 경우, 시간 동기화가 중요하기 때문에 각 서버간 Network Time Protocol로 시간을 동기화 해야한다.
	- id 동기화를 위해 zookeeper 등 사용이 필요할 듯 하다
## Appendix
---
- [[UUID vs auto_increment ID in RDBMS]]
- [Announcing Snowflake (twitter.com)](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake)
- https://code.flickr.net/2010/02/08/ticket-servers-distributed-unique-primary-keys-on-the-cheap/