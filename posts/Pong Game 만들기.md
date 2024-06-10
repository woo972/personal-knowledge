---
tags:
  - coding_challenge
  - javascript
  - html5
  - canvas
  - dev
dg-publish: true
---
## Info
---
- 완성작: https://github.com/woo972/simple_pong_game
## Lesson & Learn
---
- HTML5에서 이미지나 애니메이션을 핸들링하기 위해서 canvas를 사용할 수 있다.
```javascript
var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d'); // this object make you do some graphic works on canvas

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

var animation;
function playCanvas(){

animation = requestAnimationFrame(playCanvas); // 프레임마다 해당 함수를 반복하게 해준다
ctx.clearRect(0, 0, canvas.width, canvas.height); // 이동하고 난 이전의 객체는 화면에서 제거한다.

// ... do something ...
}

playCanvas();

if(gameOver){
	cancelAnimationFrame(animation);
}
```
- javascript에서도 class를 사용할 수 있다.
```javascript
class Person {
	constructor(name, age){
		this.name = name;
		this.age = age;
	}
	isAdult(){
		return this.age > 20;
	}
}
```
- javascript에서 enum과 같은 데이터타입을 사용하려면, Object.freeze()를 사용해야한다. 
```javascript
const MOVE = {
	STOP : 'STOP',
	UP : 'UP',
	DOWN : 'DOWN'
}
Object.freeze(MOVE);
```
- 게임을 만들기 위해서 중요한 개념
	- 화면에 오브젝트를 생성한다 (예로 canvas 활용)
	- 프레임마다 코드를 실행한다 (화면 리프레쉬, 오브젝트 생성, 이벤트 수신 등)
	- 충돌을 체크한다 (오브젝트간 충돌을 어떻게 감지하고 어떤 이벤트를 발생시킬 것인가?)
- 발전이 필요한 부분
	- 자바스크립트 기본 개념을 대부분 잊어버려 공부가 필요함
	- 클래스, 상속, 오버라이딩 등을 자바스크립트에서 어떻게 하는지 공부해야 함
	- 모던 자바스크립트(es6) 이상으로 구현하려면 어떤 부분이 필요한지 공부해야함
	- 게임을 만들기 위해서는 물리엔진 등의 라이브러리가 있을 텐데 확인 필요함
	- 
## Appendinx
---
- 코딩 챌린지: https://github.com/lolo8304/coding-challenge#write-your-own
- 크롬 공룡 게임 만들기: https://www.youtube.com/watch?v=qkTtmgCjHhM