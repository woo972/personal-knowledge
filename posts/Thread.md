---
tags:
  - dev
  - java
  - thread
  - async
  - concurrency
dg-publish: true
---
## Thread란
---
Java의 thread는 프로그램에서의 thread와 매칭되는 클래스이다. JVM은 다수의 thread를 병렬적으로 실행시킬 수 있다. JVM이 시작되면 주로 main 메서드가 실행되면서 하나의 non-daemon thread가 실행된다. thread별로 우선순위가 있으며, 어떤 thread에서 수행되는 코드가 새로운 thread를 생성했다면 동일한 우선순위를 가지게 된다. 
## Thread의 생성
---
thread를 생성(즉, 호출하는 인스턴스가 잠재적으로 현재 thread와 다른 thread에서 실행)하기 위해서는 두가지 방법이 있는데 하나는 Thread 클래스의 서브클래스를 만드는 방법이고 다른 하나는 Runnable 인터페이스를 구현하는 방법이 있다. (Thread 클래스 자체도 Runnable 구현)
```java
class CustomThread extends Thread {
	public void run(){
		... doSomething ... 
	}
}

class CustomThread2 implements Runnable {
	public void run(){
		... doSomething ...
	}
}
```

Runnable의 run method는 리턴값이 없고 checked exception을 던지지 못하는데, 이를 위해 Callable 인터페이스를 구현하는 방법이 있다.
```java
class CustomThread3 implements Callable<V> { // V는 리턴 타입
	V call() throws Exception;
}
```
## Thread의 종료
---
Java의 Thread 클래스에 대한 설명을 보면, JVM은 몇 가지 상황이 발생하기 전까지 thread를 수행한다.
- Runtime 클래스의 exit()가 호출되고 security manager가 exit 명령을 수락하는 경우
- daemon thread가 아닌 모든 thread가 죽는 경우(즉, daemon thread는 프로그램 종료여부와는 관련이 없다)
- run method에 호출을 리턴하는 경우
- run method에 예외를 발생시켜 전파하는 경우
## Thread의 상태
---
Thread의 Nested class인 `Thread.State` enum을 통해 thread의 생명주기를 확인해볼 수 있다. 
- NEW: thread가 아직 시작되지 않은 상태 `new Thread()`
- RUNNABLE: JVM에 의해 실행될 준비가 된 상태. OS의 다른 리소스(프로세서 등)를 기다리고 있을 수 있다. `start()`
- BLOCKED: synchronized 블록이나 메서드에 진입하기 위해 monitor lock 권한을 대기하는 상태. 
- WAITING: 다른 thread가 특정한 동작을 하기를 기다리는 상태. 아래와 같은 메서드가 호출될 때 이 상태가 된다.
	- timeout 없는 `Object.wait()`: 어떤 object에 대해 이 메서드를 호출한 thread는 다른 thread가 해당 object에 대해 `Object.notify()` 또는 `Object.notifyAll()`을 호출할 때 까지 대기한다. 
	- timeout 없는 `Thread.join()`: 이 메서드를 호출한 thread는 특정한 thread가 종료될때까지 기다린다.
	- `LockSupport.park`
 *  TIMED_WAITING: 다른 thread가 특정한 동작을 하기 기다리는 상태. 특정한 시간동안 대기한다. 아래와 같은 메서드가 호출될 때 이 상태가 된다.
	 * `Thread.sleep`
	 * timeout을 설정한 `Object.wait()`
	 * timeout을 설정한 `Thread.join()`
	 * `LockSupport.parkNanos`
	 * `LockSupport.parkUntil`
 * TERMINATED: thread 실행이 완료되어 종료된 상태.
![[Pasted image 20231202183037.png]]
[[Thread State]]
## Thread Lock
---
모든 객체는 Synchronization을 위한 Monitor Lock(Intrinsic Lock)을 가지고 있다. (통상 줄여서 Monitor라고 함) thread는 객체에 접근하기 위해 monitor를 획득하여야 한다. 이는 다음과 같은 두가지를 보장한다.
- 객체의 상태에 배타적인 접근을 강제한다.
- Visibility(가시성)을 보장하기 위해 선행관계(happens-before relationship)를 만든다. 

thread가 synchronized 메서드에 진입하면 monitor lock을 얻고 메서드에서 정상적으로, 혹은 exception에 의해 반환될 때 monitor lock을 반납한다. synchonized static method에 대한 의 경우, 객체에 직접 lock을 거는 것이 아니라 Class 객체에 lock을 거는 것이기 때문에 class의 인스턴스를 위한 lock과 구분되는 다른 lock에 의해 class의 static field가 관리된다.


## 참고
---
[[Daemon Thread]]
[[Checked - Unchecked Excpetion]]