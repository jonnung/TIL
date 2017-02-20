# CORS (Cross Origin Resource Sharing)
## 개요
브라우저에서는 javascript 의 XMLHttpRequest 를 통한 다른 도메인의 자원을 요청할 수 없도록 제한한다. (Same Origin Policy, SOP)  
하지만 최근 웹 어플리케이션 구현에서는 다른 도메인의 접근 해야하는 상황이 많이 발생하기도 한다.  
GET 요청에 한해서는 [JSONP](https://en.wikipedia.org/wiki/JSONP) 를 사용하기도 하지만 직접 개발해서 운영하는 API 서비스가 아니라면 JSONP 를 지원하는지 여부가 달라질 수 있다.  
그래서 W3C 에서 Cross-Origin Resource Sharing (CORS) 권고사항을 만들었고, 브라우저에서 이를 지원하고 있다.  

## 종류
- Simple
- Preflight
- Credential
- Non-Credential
