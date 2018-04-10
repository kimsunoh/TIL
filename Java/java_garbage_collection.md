# Garbage Collection (GC, ������ �÷���)
- ���̻� �ʿ���� (������)��ü�� ã�� ����� �۾��� ��
- weak generational hypothesis�� ���Ѵ�
	- ��κ��� ��ü�� �ݹ� ���� �Ұ��� ����(unreachable)�� �ȴ�
	- ������ ��ü���� ���� ��ü���� ����� ���� ����
	- ������ ������ �ִ��� �츮�� ���� HotSpot VM������ ũ�� 2���� ������ �������� ��������

## stop-the-world
- GC�� �����ϱ� ���� JVM�� ���ø����̼� ������ ���ߴ� ��
- �߻��ϸ� GC�� �����ϴ� �����带 ������ ������ ������� ��� �۾��� ����
- GC �۾��� �Ϸ��� ���Ŀ��� �ߴ��ߴ� �۾��� �ٽ� ������
- � GC�˰����� ����ϴ��� �߻���
- �밳�� ��� GCƩ���̶� �� stop-the-world �ð��� ���̴� ��
	- Java�� ���α׷� �ڵ忡�� �޸𸮸� ��������� �����Ͽ� �������� ����

## HotSpot VM�� 2���� ���� ����
- Young Generation
	- ���Ӱ� ������ ��ü�� ��κ��� ��ġ��
	- �̿������� ��ü�� ����� �� Minor GC�� �߻��Ѵٰ� ����
- Old Generation
	- ���� �Ұ��� ���·� ���� �ʾ� Young �������� ��Ƴ��� ��ü�� ����� �����
	- ��κ� Young �������� ũ�� �Ҵ��
	- Young�������� GC�� ���� �߻���
	- �� �������� ��ü�� ����� �� Major GC(Ȥ�� Full GC)�� �߻�

### ������ �̵� �帧
- -( Allocation )-> [Young Generation] -(Promotion)-> [Old Generation],[Permanent Generation]
* Permanent Generation ���� ( Perm ���� )
	- ~Method Area ��� ��(?)~
	- JVMŬ������ �޼��� ��ü�� ���� ����
	- JVM�� ��� ��������� �����ϴ� ������ ����
	- Runtime constant pool�� �� Ŭ������ ���� �����ڿ� �޼���鿡 ���� �ڵ带 ����
		* Runtime constant pool 
			- �� Ŭ������ ���� �ν��Ͻ� ������ �ν��Ͻ��� ��� ����, static ������ static �ν��Ͻ��� ������� ����Ǵ� ����
			- Method area�� ���� �Ҵ�ǰ� ������, JVM�� ��� ��������� �����ϰ� ��
	- ���⼭ GC�� �߻��ϸ� Major GC�� Ƚ���� ���Ե�

#### ī�����̺�
- Old������ 512����Ʈ�� ���(chunk)�� �Ǿ��ִ� ���̺�
	- Old���� ��ü�� Young ���� ��ü�� ������ ������ ������ ǥ�õ�
- Young ������ GC�� ������ ���� Old ������ �ִ� ī�����̺� ������ GC ������� �ĺ���
- write barrier�� ����Ͽ� ������
	- Minor GC�� ������ �� �� �ֵ��� �ϴ� ��ġ
	- �ణ�� �������� �߻������� �������� GC �ð��� �پ��� ��

## Young ����
- 3���� �������� ����
	- Eden ����
	- Survivor ����(2��)
- GC ó�� ����
	1. ���� ������ ��κ��� ��ü�� Eden ������ ��ġ��
	2. Eden �������� GC�� �� �� �߻��� �� ��Ƴ��� ��ü�� Survivor ���� �� �ϳ��� �̵� ��
	3. Eden �������� GC�� �߻��ϸ� �̹� ��Ƴ��� ��ü�� �����ϴ� Survivor �������� �̵� ��
		1) ������ Survivor ������ �ƹ� �����͵� ���� ���°� ��
		* ��, Survivor ���� �� �ϳ��� �ݵ�� ����ִ� ���¿�����
		* �� Survivor ������ ��� �����Ͱ� �����ϰų�, �� ���� ��� ��뷮�� 0�̸� �ý����� ���������� ��
	4. 1-3������ �ݺ��ϴٰ� ����ؼ� ��Ƴ��� �ִ� ��ü�� Old�������� �̵��ϰ� ��

### MinorGC
- GC ���� ���
	1. MinorGC�� �߻��ϸ� Eden�� S1�� Alive �Ǿ��ִ� ��ü�� S2�� ������
		- S1�� Alive �Ǿ����� ���� ��ü�� �ڿ��� S1�� �����ְԵ�
	2. S1�� Eden ������ Clear��
	3. Minor GC�� �����ϴٰ� Survivor �������� ������ ��ü�� Old �������� �̵�
	
## Old ����
- �����Ͱ� ���� ���� GC�� ������

### Full GC
: Mark & Compact �˰��� �̿�
- ������
	1. ��ü ��ü���� reference�� �� ���󰡸� reference�� ������� �ʴ� ��ü�� Mark ��
	2. 1�۾��� ������ Mark�� ��ü�� ������
		: �����δ� Compact��� �ؼ�, Mark�� ��ü�� ����� �κ��� ����ϴ� ��ü�� �޲پ� ������
- Full GC�� �ſ� �ӵ��� ����
- Full GC�� �Ͼ�� ���߿� ���������� stop-the-world�� �߻��Ѵ�

## JVM�� GC�� ���
### Serial GC (-XX:+UseSerialGC, ���� S-GC)
- ����ũ���� CPU �ھ �ϳ��� ���� �� ����ϱ� ���ؼ� ���� ���, ����ϸ� �ȵ�
- Old ������ GC�� mark-sweep-compact��� �˰����� �����
	- mark-sweep-compact
		1. Old ������ ����ִ� ��ü�� Mark��
		2. Heap�� �� �κк��� Ȯ���Ͽ� ��� �ִ� �͸� ����(Sweep)
		3. �� ��ü���� ���ӵǰ� ���̵��� ���� ���� �� �κк��� ä���� ��ü�� �����ϴ� �κа� ��ü�� ���� �κ����� ����(Compaction)
- CPU �ھ� ������ ���� �޸𸮰� ���� �� ������ ���

### Parallel GC(-XX:+UseParallelGC, ���� P-GC)
: Throughput GC ��� ��
- S-GC�� �⺻���� �˰����� ����, �׷��� S-GC�ʹ� �ٸ��� Parallel GC�� ó���ϴ� �����尡 ������
	- S-GC���� ������ ��ü�� ó���� �� ����
- �޸𸮰� ����ϰ� �ھ��� ������ ���� �� ������
	
### Parallel Old GC(-XX:+UseParallelOldGC)
- P-GC�� ���Ͽ� Old������ GC �˰��� �ٸ�
- Mark-summaty-Compaction �ܰ踦 ��ħ
	1. Summary�ܰ�
	: �ռ� GC�� ������ ������ ���ؼ� ������ ����ִ� ��ü�� �ĺ��Ѵٴ� ������ Mark-Sweep-Compaction �˰����� Sweep �ܰ�� �ٸ�
	
### CMS GC(-XX:+UseComcMarkSweepGC)
: Low Latency GC��� ��
- ����ܰ�
	1. Initial Mark �ܰ�
		- Ŭ���� �δ����� ���� ����� ��ü �� ��� �ִ� ��ü�� ã�� ������ ����
		- stop-the-world �ð��� �ſ� ª��
	2. Concurrent Mark �ܰ�
		- ��� ����ִٰ� Ȯ���� ��ü���� �����ϰ� �ִ� ��ü���� ���󰡸鼭 Ȯ����
		- �� �۾��� �ٸ� �����尡 ���� ���� ���¿��� ���ÿ� �����
	3. Remark�ܰ�
		- Concurrent Mark �ܰ迡�� ���� �߰��ǰų� ������ ���� ��ü�� Ȯ����
	4. Concurrent Sweep �ܰ�
		- �����⸦ �����ϴ� �۾��� ������
		- �ٸ� �����尡 ����ǰ� �ִ� ��Ȳ���� ������
- stop-the-world �ð��� �ſ� ª��
- ��� ���ø����̼��� ���� �ӵ��� �ſ� �߿��� �� CMS GC�� ���
- ����
	- �ٸ� GC ��ĺ��� �޸𸮿� CPU�� �� ���� �����
	- Compaction �ܰ谡 �⺻������ �������� ����
		- ������ �޸𸮰� ���� Compaction �۾��� �����ϸ�, �ٸ� GC ����� stop-the-world �ð��� �� ��� ������ Compaction �۾��� �󸶳� ����, �������� ����Ǵ��� Ȯ�� �ʿ�

### G1 GC
: Young �������� �����Ͱ� Old �������� �̵��ϴ� �ܰ谡 ����� GC ����̶�� �����ϸ� ��
- CMS GC�� ��ü�ϱ� ���ؼ� �������
- ����
	- ������ ����� GC�� �߿��� ���� ������
		- JDK 7�������� ���� ���Ե�

## GC Algorithms
### Default Collector
- Minor GC�� Scavenge, Major GC�� Mark&compact �˰����� ����ϴ� ���

### Parallel GC
- Minor GC�� ���ÿ� �������� Thread�� �̿��ؼ� GC�� �����ϴ� ���
- �˼��� 4CPU�� 256M ������ �޸𸮸� ���� HW���� ������
	- 1CPU�� ��� MutiThread�� ���� �ڿ��̳� ������ ���ؼ� CPU Power�� ���Ǳ� ����, ��ȿ��
- ��� ���� �ɼ�
	- Low-pause, Throughput ����� ����
- ������ ���� ���� �ɼ�
	- XX:ParallelGCThreads 
	- ��� Thread�� �̿��Ͽ� Parallel GC�� ���Ǵ� Thread�� �� ���� ����

#### Low-pause ���
- CMS, G1 �� ����� ����
	- CMS�� ���Ʃ���� �䱸��
	- G1�� JDK 7������ ���뼺 ���ķ� ����� �������� ������, JDK 9������ Default
- FullGC�� �߻��Ҷ� Concurrent GC ����� �Բ� ��밡��
- GC�� ���� �ϴ� ���� �ƴ϶� Stop-the-world�� �ּ�ȭ �ϴµ� ������ ��

#### Throughput ���
- MinorGC�� �߻����� �� �������� �ϵ��� ����ó�� �ϴµ� ������ ��
	- Major GC�� �� Mark&Compact ���(Default)�� ����ϵ��� ��

### Concurrent GC
- Full GC�� ���ؼ� �߻��ϴ� Stop-the-world ������ �ּ�ȭ�ϱ� ���� GC ���
- �Ϻδ� Application�� ���ư��� �ܰ迡�� �Ϻ� FullGC�� ����, �ּ����� GC�۾��� Application�� ������ �� ����
- stop-the-world ���¿��� initial-mark, remark �۾��� ����

### Incremental GC ( Train GC )
- Full GC�� ���ؼ� �߻��ϴ� Stop-the-world ������ �ּ�ȭ�ϱ� ���� GC ���
- Minor GC�� �Ͼ������ Old������ ���ݾ� GC��
	- Full GC�� �߻��ϴ� Ƚ��, �ð��� �پ�� ( �̷л� )
- �������� ��찡 ���� �� �����Ƿ� �ݵ�� �׽�Ʈ �� ����ϱ�

---
## ������
* [NAVER D2 - Java Garbage Collection](http://d2.naver.com/helloworld/1329)
* [Understanding the G1 Garbage Collector ? Java 9](https://www.dynatrace.com/news/blog/understanding-g1-garbage-collector-java-9/)
* [JVM �޸𸮱���](http://huelet.tistory.com/entry/JVM-%EB%A9%94%EB%AA%A8%EB%A6%AC%EA%B5%AC%EC%A1%B0)
* [JVM PermGen ? where art thou?](https://dzone.com/articles/jvm-permgen-%E2%80%93-where-art-thou)
* [�ڹ� �� ���α׷��� - JVM memory�� GC ����](https://www.slipp.net/wiki/pages/viewpage.action?pageId=26641949)
* [Java Reference�� GC](http://d2.naver.com/helloworld/329631)
* [JVM GC�� �޸� Ʃ��](http://levin01.tistory.com/441)
* [JVM�� Garbage Collection](https://www.holaxprogramming.com/2013/07/20/java-jvm-gc/)
