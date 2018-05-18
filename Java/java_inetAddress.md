# InetAddress
- IP�ּҸ� ��Ÿ���� Ŭ����
- static���� �⺻���� ȣ��Ʈ�� �̸�, IP ���� �� �� �ִ�

## InetAddress vs Inet4Address vs Inet6Address
- ipv4 vs ipv6 �� ����

## getHostName()
```java

System.out.print( InetAddress.getLocalHost().getHostName() );
// localhost
```
- localhost�� ����� ����

## ��ü
```java
System.out.print( System.getenv("HOSTNAME") );
// xxx.xxx.com
```
- �ý��� Ŭ������ �̿��� ������ ȯ�溯������ �̿�

---
## ����ũ
* [Java Docs](https://docs.oracle.com/javase/8/docs/api/java/net/InetAddress.html)
