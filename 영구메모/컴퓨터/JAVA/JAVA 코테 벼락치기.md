|                 |                         |
|:----------------|:------------------------|
|   작성일           |   2023-04-16   |
|     분류          |                         |
| 태그              | #작성중                         |  

# 주석
---
- 라인주석 : `//`
- 범위 주석 : `/* */`

# 문자열
---
```java
str.length() // 문자열 길이 반환

str.isEmpty() //문자열이 비었는지 확인

str1.equals(str2) // 문자열을 비교할때 사용

str1.compareTo(str2) // 문자열을 사전순으로사전 순으로 비교한다.
//str1이 str2보다 사전 순으로 앞인 경우 -1, 같은 경우 0, 뒤인 경우 1을 반환 

str.indexOf('c') // 문자열 'c'의 인덱스를 반환 

str.lastIndexOf('c') // 문자열 'c'의 마지막 인덱스를 반환

str.subString(start, end) // start인덱스부터 end-1인덱스까지 문자열 자르기

str1.concat(str2) // 문자열 합치기 

str.replace('변경될 문자열', '변경할 문자열') // 변경될 문자열을 변경할 문자열로 바꿔준다.

str.contains('k') // str문자열에  k라는 문자가 있는 경우 true반환

str.split(" ") // 괄호안의 매개변수를 기준으로 문자열 자르기 

str.trim() // 문자열의 앞, 뒤의 공백을 제거

variable.toString() // int형 변수를 string으로 변환

str.parseInt() // 문자형 변수 str을 int형으로 변경

str.append()  // 문자열 더하기
str1 + str2 //문자열 더하기

str.chartAt(2) // 2번째 문자 return
```

## String Builder

```java
StringBuilder sb = new StringBuilder("Default String"); // 선언

sb.length() // 문자열 길이

sb.capacity() // 현재 사용하는 용량

sb.append("asdflasdf") // 문자열 덧붙이기

sb.reverse() // 문자열 뒤집기

sb.replace(0, 1, "A") // 123456 => A23456

sb.setCharAt(1, 'c') // 문자 교체

sb.substring(0, 2) // 문자열 자른 값 return

sb.toString() // String 값 return
```
# 배열
---
```java
int[] arr = new int[N]; //길이 N만큼의 배열 생성

int[][] arr2 = new int[N][M]; //N * M 만큼의 배열 생성

arr.add() //배열에 데이터 추가

arr.length //배열 길이 확인 : 5

List<String> str = new ArrayList<String>(); //ArrayList 사용
str.add("test");

str.size() //ArrayList 길이 조회

AL.indexOf(value) // value 가 있다면 index, 없으면 -1

Arrays.sort(배열) // 정렬
Arrays.sort(배열,Collections.reverseOrder()); // 내림자순 정렬
```

# HashMap
---
```java
Map<Integer, String> map = new HashMap<>();  // HashMap 선언

map.put(1, "Java"); // 데이터 삽입

map.remove(4); // 키 삭제

System.out.println(map.containsValue("Java")); // 값 있는지 확인, return true or false

mapTest.get(1) // 키의 값 확인

map.getOrDefault("c","-999"); // 키가 없다면 default 값 적용

map.replace(A, B) // A의 값을 B로 replace 함
```

# for-loop
```java
for(자료형 변수명 : 배열명) // 향상된 for 문
{
	코드
}
```

# Stack
---
```java
Stack<Integer> stack = new Stack<>(); //스택 선언

stack.push(1) // 값 추가

stack.pop() // 값 제거

stack.clear() // 스택 초기화

stack.peek() // 가장 상단의 값 확인

stack.contains(1) // stack 에 1이 있는 지 확인

stack.size() // stack의 크기 출력
```

# Queue
---
```java
Queue<Integer> queue = new LinkedList<>();
Queue<String> queue = new LinkedList<>();

queue.add(1) // 값 추가 (예외 발생 O)
queue.offer(1) // 값 추가 (예외 발생 X)

queue.remove() // 값 제거 (예외 발생 O)
queue.poll() // 값 제거 (예외 발생 X)

queue.element() // 다음 값 확인 (예외 발생 O)
queue.peek() // 다음 값 확인 (예외 발생 X)
```

# Deque
---
```java
Deque<Integer> dq = new LinkedList<>();
Deque<Integer> dq = new ArrayDeque<>(); // LinkedList 보다 사용 권장 됨

dq.add() // 마지막에 원소 삽입
dq.addLast() // 마지막에 원소 삽입

dq.addfirst() // 첫 부분에 원소 삽입

dq.offer() // 마지막에 원소 삽입 (예외 X)
dq.offerLast() // 마지막에 원소 삽입 (예외 X)

dq.offerFirst() // 첫 부분에 원소 삽입 (예외 X)

dq.remove() // 맨 앞 원소 제거
dq.removeFirst() // 맨 앞 원소 제거

dq.removeLast() // 맨 뒤 원소 제거

dq.poll() // 맨 뒤 원소 제거 없으면 null return
dq.pollLast() // 맨 뒤 원소 제거 없으면 null return

dq.pollFirst() // 맨 앞 원소 제거, 없으면 null return

```

# Math
---
```java
Math.pow(5, 2) // 5의 제곱

Math.abs(-123) // 123
```


# 자료형
---
```java
Boolean // true, false
```

# HashSet
---
```java
HashSet set = new HashSet<Integer>();

set.add(3) // 원소 추가

set.size() // 크기 구하기

set.contains(3) // true or false
```

# Heapq
---
```java
PriorityQueue<Integer> heapq = new PriorityQueue<>();

heapq.add() // 추가
heapq.offer() // 추가 (예외 x)

heapq.poll() // 값을 return 하고 제거한다. 비어있다면 null return

heapq.remove(Object o) // 제거

heapq.peek() // 다음 원소 확인

heap.size() // 크기 확인

heap.toArray(new Integer[0]) // Integer 형 배열 변환
```
# 관련 링크
---


# 출처
---