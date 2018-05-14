# BlockingQueue
- Produce-Consumer pattern�� ��������� Multi Thread ������ ���� �� �ϳ�
- Ư�� ��Ȳ���� �����带 ����ϵ��� �ϴ� ť�� ó�� ����
	- Ư����Ȳ
		- Dequeue �� ť�� ������� ��
		- Inqueue �� ť�� �� ������ ��
	- �ٸ� �����尡 ��Ȳ�� �ذ��� �� ������ �����¸� �����Ѵ�

## BlockingQueue�� ����
: java ���� ������ ���ŷ ť�� ����ü

### ArrayBlockingQueue
- �����迭�� �Ϲ����� Queue�� ������ Ŭ����, ���� �� ũ�� ���� �Ұ�
- ��á�� �� inqueue, ����� �� dequeue�� ���� ������ block
- ������ ������

#### Ư¡
- ������ ���� ��å�� �ΰ�, block�� thread���� ������ ��⿭�� �����Ѵ�
- ��⿭ ó���� ���� ��Ȯ�� ���� ������ �ȵȴ�

### LinkedBlockingQueue
- ���������� bound�� ������ Linked list�� ������ Queue
- capacity�� �ʱ⿡�� �������� �ʴ� ��� integer.MAX_VALUE�� �ڵ� �����ȴ�
	- node�� �������� ���Խø��� �����ȴ�

### PriorityBlockingQueue
- PriorityQueue�� ���� ���� ����� ���� �뷮������ ���� Queue
	- dequeue�� ���� block����� ���´�
	- unBounded �̹Ƿ�, �۾� ������ fail�� ���� �ڿ����� �� ��

#### Ư¡
- null element �� non-comparable object�� �������� ������, natural ordering�� ������

### SynchronousQueue
- �������� thread�� object�� queue�� ���� ������ �ٸ� ����ִ� ������ object�� queue�� ���� ���۰� sync-up�Ǿ�� �ϴ� handoff design�� �����ϴ�
	- �ַ� information, event, task�� ���� �Ѵ�
- Collection �Լ��鿡 emepty collection���μ��� �������� ���Ѵ�
	
#### Ư¡
- Queue ���η��� insert �۾��� �ٸ� �������� remove �۾��� �ݵ�� ���ÿ� �Ͼ���Ѵ�
	- remove �۾��� ����, insert �۾��� �־�߸� ����ȴ�
- ���� ��Ī�Ǵ� �۾��� ���� ��� ���� ������ ����Ѵ�
- ���� �� ���� �����Ƿ� �����Լ� ����� �Ұ����ϴ�
- poll()�� �������� �� ���� �õ��� thread�� ������ null�� return�Ѵ�

---
## ����ũ
- [���ŷ ť(Blocking Queues)](http://parkcheolu.tistory.com/29)
- [[Java]BlockingQueue�� ������ ���](http://oniondev.egloos.com/558949)
- [Class LinkedBlockingQueue<E>](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingQueue.html)
