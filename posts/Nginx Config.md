---
tags:
  - dev
  - middleware
  - nginx
  - configuration
dg-publish: true
---
## Redirection by `rewrite`
---
nginx의 config 파일 내 server.location 항목에 rewrite를 통해 redirect를 설정할 수 있다.
### format
```
rewrite <old> <new> <flag>
```
### flag
- `permanent` status code 301로 영구적으로 new url로 이동시킨다는 의미이다.
- `temporary` status code 302로 new url로의 이동은 임시적이며, 향후 원래대로 돌아갈 수도 있다는 의미이다.
- `last`는 해당 rewrite rule과 매칭했을 때, 나머지 rule은 적용하지 않고 끝낸다는 의미이다.
### 예시
```
server {
	listen 80;
	server_name m.{{getenv "DOMAIN"}};
	root /com/program/nginx/html;
	include status.conf;
	location / {
		rewrite ^/m/promotion/downloadcoupon\.com$ http://promotion.{{getenv "DOMAIN"}}/download-coupon permanent;
	}
}
```
## Block non valid requests
---
- robot.txt를 통해 crawler에게 open된 url과 비공개 url을 알려줄 수 있다. 단, 이 파일을 이용해서 request를 block해서는 안된다.
- location 블록에서 request block 설정을 할 수 있다.
### 예시
```
location / {
	if($arg_param="") { // request의 query가 empty인 경우,
		return 400; // 400 bad request를 반환한다
	}
}
```
```
location /users/ {
	if($uri ~* "(.*)/null(.*)"){ // request path에 null이 들어간 문자열이 있으면,
		return 400; // 400 bad request를 반환한다
	}

	access.log off // access.log에 남기지 않는다
}
```
## Variable
---
- `$uri`: path와 query를 포함하는 request URI를 의미한다.
- `arg_param`: request는 query value를 의미한다. 
	- 예) `http://example.com?query=value` 에서 value를 의미