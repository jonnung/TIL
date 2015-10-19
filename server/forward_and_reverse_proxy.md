# Forward Proxy
- 클라이언트가 example.com 에 접근 하려고 하면 클라이언트가 직접 연결하는게 아니라 Forward proxy가 클라이언트의 요청을 받고, proxy가 example.com에 연결하여 응답 결과를 받아와 다시 클라이언트에 전달(forward)
- Forward proxy 는 대개 Cache 기능이 있으므로 자주 사용하는 컨텐츠를 캐시하면 성능 향상을 기대할 수 있음.
- 기업 환경에서 많이 사용함

# Reverse Proxy
- 클라이언트가 example.com에 접근 하려고 하면 Reverse proxy가 이 요청을 받아서 내부 서버에서 데이터를 받아와 클라이언트에게 전달
- Reverse proxy를 두는 이유는 보안 때문
- 대개 WAS(Web Application Server)는 DB서버와 연결되므로 WAS가 해킹을 당하면 DB서버도 위험할 수 있음.  따라서 Reverse proxy를 두고 WAS를 내부망에 위치시켜 Reverse proxy 서버만이 내부에 있는 WAS와 통신해서 결과를 받아올 수 있는 구조.

----
![forward_and_reverse_proxies](http://community.brocade.com/legacyfs/online/1914_fwdrevproxy.png)  
(이미지 출처: [Using Stingray Traffic Manager as a Forward Proxy](http://community.brocade.com/t5/vADC-Docs/Using-Stingray-Traffic-Manager-as-a-Forward-Proxy/ta-p/73721))
