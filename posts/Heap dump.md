---
tags:
  - dev
  - incident
  - thread
  - heap
dg-publish: true
---
## heap dump
---
- heap의 사용량이 늘어나는 경우 -> memory 사용량이 늘어나는 경우
- (위의 이유로 인해) gc사용량이 늘어나는 경우
- (위의 이유로 인해) OOM이 발생하여 어플리케이션이 죽는 경우
- 어플리케이션이 죽으면 heap dump를 생성하지 못하므로, JVM option을 통해 OOM을 대 비할 수 있다.
	- -XX: +HeapDumpOnOut0fMemoryError -XX: HeapDumpPath=/heapdump. hprof
	- path를 지정하지 않으면 jvm 시작 디렉토리에 남게된다
	- -XX: +PrintClassHistogramAfterFullGC, XX: +printClassHistogramBeforeFulLGC 로 FullGC 전후 메모리 상태도 체크 가능 하다
- heap dump를 뜨게 되면 어플리케이션이 멈출 수 있으므로, 서버가 요청을 받지 않게 만든 후에 실시한다. (jmap 명령어 등 참조)
- 할당된 heap size 확인: 
	- `jps -vm`으로 jvm 파라미터 확인
	- `jcmd <pid> GC.heap_info`로 할당된 메모리 확인
