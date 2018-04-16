## jstat
- HotSpot JVM�� �ִ� ����͸� ����
 | 	- jstat �̿ܿ� HotSpot JVM ����͸� ������ jps, jstatd�� ����
- GC��������, Ŭ�����δ� ���� ����, Just-in-Time �����Ϸ� ���� ���� ���� �� �� ����

### jstat ��ġ
- $JAVA_HOME/bin
- java, javac�� ���� ��ġ�� ����

### Options
| �ɼ�        | ���  |
| ------------- |:-------------:| 
| gc      | �� Heap ������ ���� ũ��� ���� ������ ��뷮(Eden, Survivor, Old ��), �� GC ���� ȸ��, ���� GC �ҿ�ð��� ������ |
| gccapacity | �� Heap ������ �ּ� ũ��(ms), �ִ� ũ��(mx), ���� ũ��, �� ������ GC ���� Ƚ���� �� �� �ִ� ������ ���� �ش�. ��, ���� ��뷮�� ���� GC �ҿ� �ð��� �� �� ����|
| gccause | -gcutil �ɼ��� �����ϴ� ������ �Բ� ������ GC ���ΰ� ���� �߻��ϰ� �ִ� GC�� ������ �� �� �ִ� ������ ������ |
| gcnew | New ������ ���� GC ���� ������ ������ |
| gcnewcapacity | New ������ ũ�⿡ ���� ��� ������ ������ |
| gcold | Old ������ ���� GC ���� ������ ������ |
| gcoldcapacity | Old ������ ũ�⿡ ���� ��� ������ ������ |
| gcpermcapacity | Permanet ������ ���� ��� ������ ���� �� |
| gcutil | �� Heap ������ ���� ��� ������ ������� ������, �� GC ���� Ƚ���� ���� GC �ð��� �� �� ���� |

### Result columns
|	Į�� | ���� | jstat �ɼ� |
| ------------- |:-------------:| -------------:| 
| S0C | Survivor 0 ������ ���� ũ�� ǥ�� ( KB ���� )	| -gc -gccapacity -gcnew -gcnewcapacity |
| S1C | Survivor 1 ������ ���� ũ�� ǥ�� ( KB ���� ) | -gc -gccapacity -gcnew -gcnewcapacity |
| S0U	| Survivor 0 ������ ���� ��뷮 ǥ�� ( KB ���� ) | -gc -gcnew |
| S1U	| Survivor 1 ������ ���� ��뷮 ǥ�� ( KB ���� ) | 	-gc -gcnew |
| EC	| Eden ������ ���� ũ�� ǥ�� ( KB ���� ) | 	-gc -gccapacity -gcnew -gcnewcapacity |
| EU	| Eden ������ ���� ��뷮 ǥ�� ( KB ���� ) | 	-gc -gcnew |
| OC	| Old ������ ���� ũ�� ǥ�� ( KB ���� ) | 	-gc -gccapacity -gcold -gcoldcapacity |
| OU	| Old ������ ���� ��뷮 ǥ�� ( KB ���� ) | 	-gc -gcold |
| PC	| Permanent������ ���� ũ�� ǥ�� ( KB ���� ) | 	-gc -gccapacity -gcold -gcoldcapacity -gcpermcapacity |
| PU	| Permanent������ ���� ��뷮 ǥ�� ( KB ���� ) | 	-gc -gcold |
| YGC	| Young Generation�� GC �̺�Ʈ �߻� Ƚ�� | 	-gc -gccapacity -gcnew -gcnewcapacity -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| YGCT	| Yong Generation�� GC ���� ���� �ð� | 	-gc -gcnew -gcutil -gccause |
| FGC	| Full GC �̺�Ʈ�� �߻��� Ƚ�� | 	-gc -gccapacity -gcnew -gcnewcapacity -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| FGCT	| Full GC ���� ���� �ð� | 	-gc -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| GCT	| ��ü GC ���� ���� �ð� | 	-gc -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| NGCMN | New Generation�� �ּ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcnewcapacity |
| NGCMX | New Generation�� �ִ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcnewcapacity |
| NGC | New Generation�� ���� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcnewcapacity |
| OGCMN | Old Generation�� �ּ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcoldcapacity |
| OGCMX | Old Generation�� �ִ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcoldcapacity |
| OGC | Old Generation�� ���� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcoldcapacity |
| PGCMN | Permanent Generation�� �ּ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcpermcapacity |
| PGCMX | Permanent Generation�� �ִ� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcpermcapacity |
| PGC | ���� Permanent Generation�� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcpermcapacity |
| PC | Permanent ������ ���� ũ�� ǥ�� ( KB ���� ) | 	-gccapacity -gcpermcapacity |
| PU | Permanent ������ ���� ��뷮 ǥ�� ( KB ���� ) | 	-gc -gcold |
| LGCC | ���� GC�� �߻� ���� | 	-gccause |
| GCC | ���� GC�� �߻� ���� | 	-gccause |
| TT | Tenuring threshold. Young ���� ������ �� Ƚ����ŭ ����Ǿ��� ���(S0 ->S1, S1->S0) Old �������� �̵� | 	-gcnew |
| MTT | �ִ� Tenuring threshold. Yong ���� ������ �� Ƚ����ŭ ����Ǿ��� ��� Old �������� �̵� | 	-gcnew|
| DSS | ������ Survivor ������ ũ�� ǥ�� ( KB ���� ) | 	-gcnew|

### ��ɾ� ��� ����
```bash
~$ jstat	-gcutil	-h5	<PID>	1000	1

# S0	S1	E	O	M	CCS	YGC	YGCT	FGC	FGCT	GCT
# 0.00	56.57	13.20	21.01	97.51	-	9	4.460		3	0.661	5.121
```

---
## ����ũ
* [NAVER D2 - Garbage Collection ����͸� ���](http://d2.naver.com/helloworld/6043)
* [Oracle docs - jstat-Java Virtual Machine Statistics Monitoring Tool](https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstat.html)
* [BLOG - [WAS] GC ����͸� �� Ʃ���ϱ�](https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstat.html)