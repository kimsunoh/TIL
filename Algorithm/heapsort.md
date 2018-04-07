# 힙정렬
- 힙트리(MinHeap,MaxHeap) 트리를 구성해 정렬하는 방식

## 특징
1. 정렬된 시퀀스를 활용해야 할 때 유용한 자료구조
2. 처음 힙을 구성할 때, 비용이 많이 든다.
3. 공간복잡도가 정렬할 자원가 동일하다. O(n)
	- 힙을 구성하는 공간외의 공간은 비교에 사용하는 공간 밖에 없다.
	- 정렬하기위해 객체를 따로 저장할 필요가 없다

## 속성
1. Heap order property
	: MaxHeap, MinHeap
2. Heap shape property
	: 완전 이진 트리 형태

## 정렬 알고리즘
1. n개의 노드 완전 완전 이진트리를 구성
2. MaxHeap을 구성함
	- 부모노드가 자식노드보다 큰 값을 가지는 완전이진트리
3. 가장 큰수부터 빼낸다.
4. 2,3 을 반복한다.


---
## 참고링크
* [위키백과 - 힙 정렬](https://ko.wikipedia.org/wiki/힙_정렬)
* [블로그 - 힙정렬(Heap Sort)](https://ratsgo.github.io/data%20structure&algorithm/2017/09/27/heapsort/)