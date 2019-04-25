# HTTPS
- TSL 위에 HTTP를 얹어 보안된 HTTP 통신을 하는 프로토콜
    - TLS/SSL 프로토콜을 이용하는 HTTP
- HTTP 통신에 Transpoer Layer Security Layer 가 추가된 것

## TSL/SSL
- 인터넷에서의 정보를 암호화해서 송수신하는 프로토콜
- HTTPS 는 SSL 인증서를 사용해서 서버와 클라이언트 간의 통신을 보증하며 암호화해서 정보를 다룬다

### 처리 방식
- 통신의 당사자가 자신을 신뢰할 수 있음을 알리기 위해 전자 서명이 포함된 인증서를 사용하고, 도청을 방지하기 위해 통신내용을 암호화 한다 
    - 보안을 확보하기 위해 두 통신 당사자 서로가 신뢰할 수 있는 자임을 확인할 수 있어야 하며, 서로간의 통신 내용이 제 3자에 의해 도청되는 것을 방지하기 위해
- 통신을 하는 사람들끼리 신원을 확인하기 위해 handshake 과정을 거친다


---
## 참고링크
- [HTTPS와 SSL 인증서](https://opentutorials.org/course/228/4894)
- [나무위키 - SSL](https://namu.wiki/w/TLS)