---
tags:
  - dev
  - cloud
  - remote
  - docker
---
## 배경
---
사내 개인 맥북에 원격으로 접속하고 싶은데, 지원되는 도커 이미지가 맥 m3에서 돌아가지 않는다.
## 스텝
---
### 오라클 클라우드 구성
#### 오라클 클라우드 회원 가입
- 신용카드 필요
- MFA 설정 필요
#### 오라클 클라우드 인스턴스 구성
- 보안그룹 구성
	- 
- 오라클 클라우드 콘솔 접속 후 '인스턴스' 클릭
- 필요 내용 기입 후 '생성' 클릭
	- ssh 접속을 위해서 private key를 다운받는다. (chmod 400 적용)
- 인스턴스 화면에서 '시작' 클릭
- (인스턴스를 삭제하고 싶은 경우, 종료 후 24시간 이후 가능)
#### 인스턴스 접속
- `ssh <private key> <user>@<host>`
	- user명과 host는 인스턴스 화면에서 '인스턴스 액세스' 란에 기입되어 있다. (나의 경우는 ocd, 158.180.90.15)
- 최초 접속 시 몇가지 안내 사항에 yes 타이핑
- 접속 완료
### 도커 설치
- centOS 기준 설치 방법: https://docs.docker.com/engine/install/centos/
- ubuntu 기준 설치 방법: https://docs.docker.com/engine/install/ubuntu/
	- sudo apt install docker-compose
### 과카몰리 구성
- // `sudo docker pull guacamole/guacd`
- // `sudo docker pull guacamole/guacamole`
- docker-compose 준비: https://github.com/mcchae/docker-guacamole 
	- port는 18080에서 80으로 변경
- `sudo ./start.sh &`
- `sudo ./initdb.sh &`
- guacamin 접속 > 신규 계정 생성(모든 권한 부여) > 재로그인 후 guacamin 삭제
- 연결설정
	- edit connection
		- protocol: VNC
	- parameters
		- network 
			- 호스트: ip
			- 포트:  port
		- authentication
			- username: 컴퓨터 로그인 아이디
			- password: 컴퓨터 로그인 패스워드
### 구글 클라우드 구성
- 구글 클라우드 가입
- Compute Engine API 사용하기
- VM인스턴스 만들기
- 리전: us-west-1(오리건) 선택
- 머신유형: e2-micro
- 부팅디스크
	- 이미지: 우분투 minimal 20.04LTS x86
	- 부팅디스크유형: 표준 영구
	- 크기: 30GB
- 방화벽: http, https 허용
	- 방화벽 규칙 5900 포트 오픈 등록 후 인스턴스 네트워크 설정에 태그 등록
- 상단 검색창에서 결제 검색 후, 예산 및 알림에서 사용량 초과 알림 설정
- `sudo apt install vim`
- 
### 맥 환경 구성
- VNC 활성화 (5900 포트)


