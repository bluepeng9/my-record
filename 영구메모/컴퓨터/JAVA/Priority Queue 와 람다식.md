|                 |                         |
|:----------------|:------------------------|
|   작성일           |   2023-04-27   |
|     분류          |                         |
| 태그              |       |  

파이썬과는 다르게 PriorityQueue를 자바로 구현하려면 코드가 많이 길어집니다. 이를 해결하기 위해 알아보는 과정을 적어봤습니다.

---
# Python 과 JAVA 코드 비교

```python
import heapq

hq = []

heapq.heappush(hq, (1, 1));
heapq.heappush(hq, (10, 2));

print(hq) # [(1, 2), (10, 2)]
```

```java
import java.util.*;

class Node {
	int idx;
	int cost;

	Node(int idx, int cost) {
		this.idx = idx;
		this.cost = cost;
	}
}

Comparator<Node> comparator = new Comparator<>() {
	@Override
	public int compare(Node o1, Node o2) {
		return o1.cost - o2.cost;
	}
};
var hq = new PriorityQueue<Node>(comparator);

hq.add(new Node(1, 1));
hq.add(new Node(10, 2));
System.out.println(hq.peek().cost); // 1
```

---

# 람다식을 이용한 짧은 코드

```java
import java.util.*;

class Node {
	int idx;
	int cost;

	Node(int idx, int cost) {
		this.idx = idx;
		this.cost = cost;
	}
}

var hq = new PriorityQueue<Node>((o1, o2) -> o1.cost - o2.cost);

hq.add(new Node(1, 1));
hq.add(new Node(10, 2));
System.out.println(hq.peek().cost); // 1
```

---
# 어떻게 람다식으로 해결 할 수 있을까?
람다식으로 해결이 가능한 이유는 다음과 같습니다.

> Interface Comparator\<T\>
>
>functional interface로, 람다식 또는 method 참조의 대상으로 할당될 수 있습니다.
>
>| Modifier and Type | Method and Description |
>|-------------------|------------------------|
>| int | compare(T o1, T o2)<br>Compares its two arguments for order. |
>| boolean | equals(Object obj)<br>Indicates whether some other object is "
>
>[Comparator (Java Platform SE 8 ) (oracle.com)](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#method.summary)

여기서 Functional interface란 오직 하나의 abstract 메서드만 갖고 있는 Interface를 의미합니다.  하지만 표에서 알 수 있듯이, Comparator는 2개의 abstract method를 갖고 있습니다. 어떻게 된 일 일까요?

다음의 Functional interface의 정의를 보면 이해할 수 있습니다.

>A functional interface is an interface that has just one abstract method (aside from the methods of Object), and thus represents a single function contract. This "single" method may take the form of multiple abstract methods with override-equivalent signatures inherited from superinterfaces; in this case, the inherited methods logically represent a single method.
>
>[java - How is Comparator\<T\> a Functional Interface? - Stack Overflow](https://stackoverflow.com/questions/63597966/how-is-comparatort-a-functional-interface)

Functional interface의 abstract 메서드의 수는 Object의 method와는 별개이므로, Comparator는 abstract 메서드 단 하나만을 갖고 있는 Interface가 됩니다.

잘못된 부분이 있으면 댓글로 알려주세요.

감사합니다.