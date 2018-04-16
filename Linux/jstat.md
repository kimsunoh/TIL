## jstat
- HotSpot JVM에 있는 모니터링 도구
 | 	- jstat 이외에 HotSpot JVM 모니터링 도구는 jps, jstatd이 있음
- GC수행정보, 클래스로더 수행 정보, Just-in-Time 컴파일러 수행 정보 등을 알 수 있음

### jstat 위치
- $JAVA_HOME/bin
- java, javac와 같은 위치에 있음

### Options
| 옵션        | 기능  |
| ------------- |:-------------:| 
| gc      | 각 Heap 영역의 현재 크기와 현재 영역별 사용량(Eden, Survivor, Old 등), 총 GC 수행 회수, 누적 GC 소요시간을 보여줌 |
| gccapacity | 각 Heap 영역의 최소 크기(ms), 최대 크기(mx), 현재 크기, 각 영역별 GC 수행 횟수를 알 수 있는 정보를 보여 준다. 단, 현재 사용량과 누적 GC 소요 시간은 알 수 없음|
| gccause | -gcutil 옵션이 제공하는 정보와 함께 마지막 GC 원인과 현재 발생하고 있는 GC의 원인을 알 수 있는 정보를 보여줌 |
| gcnew | New 영역에 대한 GC 수행 정보를 보여줌 |
| gcnewcapacity | New 영역의 크기에 대한 통계 정보를 보여줌 |
| gcold | Old 영역에 대한 GC 수행 정보를 보여줌 |
| gcoldcapacity | Old 영역의 크기에 대한 통계 정보를 보여줌 |
| gcpermcapacity | Permanet 영역에 대한 통계 정보를 보여 줌 |
| gcutil | 각 Heap 영역에 대한 사용 정도를 백분율로 보여줌, 총 GC 수행 횟수와 누적 GC 시간을 알 수 있음 |

### Result columns
|	칼럼 | 설명 | jstat 옵션 |
| ------------- |:-------------:| -------------:| 
| S0C | Survivor 0 영역의 현재 크기 표시 ( KB 단위 )	| -gc -gccapacity -gcnew -gcnewcapacity |
| S1C | Survivor 1 영역의 현재 크기 표시 ( KB 단위 ) | -gc -gccapacity -gcnew -gcnewcapacity |
| S0U	| Survivor 0 영역의 현재 사용량 표시 ( KB 단위 ) | -gc -gcnew |
| S1U	| Survivor 1 영역의 현재 사용량 표시 ( KB 단위 ) | 	-gc -gcnew |
| EC	| Eden 영역의 현재 크기 표시 ( KB 단위 ) | 	-gc -gccapacity -gcnew -gcnewcapacity |
| EU	| Eden 영역의 현재 사용량 표시 ( KB 단위 ) | 	-gc -gcnew |
| OC	| Old 영역의 현재 크기 표시 ( KB 단위 ) | 	-gc -gccapacity -gcold -gcoldcapacity |
| OU	| Old 영역의 현재 사용량 표시 ( KB 단위 ) | 	-gc -gcold |
| PC	| Permanent영역의 현재 크기 표시 ( KB 단위 ) | 	-gc -gccapacity -gcold -gcoldcapacity -gcpermcapacity |
| PU	| Permanent영역의 현재 사용량 표시 ( KB 단위 ) | 	-gc -gcold |
| YGC	| Young Generation의 GC 이벤트 발생 횟수 | 	-gc -gccapacity -gcnew -gcnewcapacity -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| YGCT	| Yong Generation의 GC 수행 누적 시간 | 	-gc -gcnew -gcutil -gccause |
| FGC	| Full GC 이벤트가 발생한 횟수 | 	-gc -gccapacity -gcnew -gcnewcapacity -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| FGCT	| Full GC 수행 누적 시간 | 	-gc -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| GCT	| 전체 GC 수행 누적 시간 | 	-gc -gcold -gcoldcapacity -gcpermcapacity -gcutil -gccause |
| NGCMN | New Generation의 최소 크기 표시 ( KB 단위 ) | 	-gccapacity -gcnewcapacity |
| NGCMX | New Generation의 최대 크기 표시 ( KB 단위 ) | 	-gccapacity -gcnewcapacity |
| NGC | New Generation의 현재 크기 표시 ( KB 단위 ) | 	-gccapacity -gcnewcapacity |
| OGCMN | Old Generation의 최소 크기 표시 ( KB 단위 ) | 	-gccapacity -gcoldcapacity |
| OGCMX | Old Generation의 최대 크기 표시 ( KB 단위 ) | 	-gccapacity -gcoldcapacity |
| OGC | Old Generation의 현재 크기 표시 ( KB 단위 ) | 	-gccapacity -gcoldcapacity |
| PGCMN | Permanent Generation의 최소 크기 표시 ( KB 단위 ) | 	-gccapacity -gcpermcapacity |
| PGCMX | Permanent Generation의 최대 크기 표시 ( KB 단위 ) | 	-gccapacity -gcpermcapacity |
| PGC | 현재 Permanent Generation의 크기 표시 ( KB 단위 ) | 	-gccapacity -gcpermcapacity |
| PC | Permanent 영역의 현재 크기 표시 ( KB 단위 ) | 	-gccapacity -gcpermcapacity |
| PU | Permanent 영역의 현재 사용량 표시 ( KB 단위 ) | 	-gc -gcold |
| LGCC | 지난 GC의 발생 이유 | 	-gccause |
| GCC | 현재 GC의 발생 이유 | 	-gccause |
| TT | Tenuring threshold. Young 영역 내에서 이 횟수만큼 복사되었을 경우(S0 ->S1, S1->S0) Old 영역으로 이동 | 	-gcnew |
| MTT | 최대 Tenuring threshold. Yong 영역 내에서 이 횟수만큼 복사되었을 경우 Old 영역으로 이동 | 	-gcnew|
| DSS | 적절한 Survivor 영역의 크기 표시 ( KB 단위 ) | 	-gcnew|

### 명령어 사용 예시
```bash
~$ jstat	-gcutil	-h5	<PID>	1000	1

# S0	S1	E	O	M	CCS	YGC	YGCT	FGC	FGCT	GCT
# 0.00	56.57	13.20	21.01	97.51	-	9	4.460		3	0.661	5.121
```

---
## 참고링크
* [NAVER D2 - Garbage Collection 모니터링 방법](http://d2.naver.com/helloworld/6043)
* [Oracle docs - jstat-Java Virtual Machine Statistics Monitoring Tool](https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstat.html)
* [BLOG - [WAS] GC 모니터링 및 튜닝하기](https://docs.oracle.com/javase/7/docs/technotes/tools/share/jstat.html)