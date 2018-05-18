# InetAddress
- IP주소를 나타내는 클래스
- static으로 기본적인 호스트의 이름, IP 등을 알 수 있다

## InetAddress vs Inet4Address vs Inet6Address
- ipv4 vs ipv6 의 차이

## getHostName()
```java

System.out.print( InetAddress.getLocalHost().getHostName() );
// localhost
```
- localhost로 결과가 나옴

## 대체
```java
System.out.print( System.getenv("HOSTNAME") );
// xxx.xxx.com
```
- 시스템 클래스를 이용해 서버의 환경변수값을 이용

---
## 참고링크
* [Java Docs](https://docs.oracle.com/javase/8/docs/api/java/net/InetAddress.html)
