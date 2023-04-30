|               |                       |
|:--------------|:----------------------|
|  작성일          |  2023-04-12  |
|    분류         |   [스케줄러 종류](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC%20%EC%A2%85%EB%A5%98.md)                    |

우선순위가 가장 높은 프로세스에게 CPU 를 줌

정수 값으로 우선순위를 표현하게 되는데, 일반적으로 리눅스에서는 작은 수가 높은 우선순위를 의미함

# Preemptive version
---
우선순위가 더 높은 프로세스가 도착시 빼앗을 수 있음

# Nonpreemptive version
---
우선순위가 더 높은 프로세스가 도착시 빼앗을 수 없음

# SJF 는 일종의 priority scheduling 이다.
---
priority = predicted next CPU burst time

# 문제점
---
- Starvation
	- 우선순위가 낮은 프로세스가 영원히 자원을 얻지 못할 수 있음
	 - Aging 으로 해결 가능
		 - 오래 기다리면 우선순위를 조금씩 높여주자

# 관련 링크
---
[Shortest-Time-First](Shortest-Time-First.md)


# 출처
---