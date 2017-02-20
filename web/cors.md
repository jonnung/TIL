# CORS (Cross Origin Resource Sharing)
## 개요
브라우저에서는 javascript 의 XMLHttpRequest 를 통한 다른 도메인의 자원을 요청할 수 없도록 제한한다. (Same Origin Policy, SOP)  
하지만 최근 웹 어플리케이션 구현에서는 다른 도메인의 접근 해야하는 상황이 많이 발생하기도 한다.  
GET 요청에 한해서는 [JSONP](https://en.wikipedia.org/wiki/JSONP) 를 사용하기도 하지만 직접 개발해서 운영하는 API 서비스가 아니라면 JSONP 를 지원하는지 여부가 달라질 수 있다.  
그래서 W3C 에서 Cross-Origin Resource Sharing (CORS) 권고사항을 만들었고, 브라우저에서 이를 지원하고 있다.  

## 요청 종류
- Simple
- Preflight
- Credential

### Simpe 요청
- 조건
  - GET, HEAD, POST 메소드만 허용
  - POST 방식일 경우 Content-type 에 허용되는 타입
    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain
  - 커스텀 헤더 허용 안함
- 서버 응답에 포함 되어야 하는 헤더
```
Access-Control-Allow-Origin: *
```

### Preflight 요청
실제 요청을 전송하기 전에 안전한지 아닌지 결정하기 위해, ```OPTIONS``` 메소드로 예비 요청을 전달.
예비 요청과 실제 요청은 개발자가 직접 지정하는게 아니라 브라우저가 아래 조건에 맞을때 자동으로 처리함.

- 조건
  - GET, HEAD, POST 를 포함한 다른 방식의 요청들도 허용
  - POST 메소드의 경우 ```application/x-www-form-urlencoded```, ```multipart/form-data``` 또는 ``` text/plain``` 이외에 다른 Content-type 으로 전송된 경우
  - 커스텀 헤더를 사용한 경우

- 예비 요청에 포함되는 헤더 (예)
```
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER
```
  - ```Access-Control-Request-Method``` 헤더는 실제 요청이 전달될 경우, POST 메소드와 함께 전송될 것임을 서버에 알림
  - ```Access-Control-Request-Headers``` 헤더는 실제 요청이 전달될 경우, X-PINGOTHER 헤더가 함께 전송될 것임을 서버에 알림

### Credential 요청
- 조건
  - ```XMLHttpRequest``` 의 ```withCredentials``` 값을 ```true``` 로 지정
  - 서버 응답 헤더에 ```Access-Contorol-Allow-Credentials: true``` 포함 해야하며, ```Access-Control-Allow-Origin``` 헤더에는 요청 Origin 을 명시해야 함

## 참고
- [https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/Access_control_CORS)
- [http://hanmomhanda.github.io/2015/07/21/Cross-Origin-Resource-Sharing](http://hanmomhanda.github.io/2015/07/21/Cross-Origin-Resource-Sharing)
