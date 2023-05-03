|                   |                                                                                   |
|:------------------|:----------------------------------------------------------------------------------|
|    작성일            |                                                                     2023-04-12    |
|      분류           |        [스케줄러 종류](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC%20%EC%A2%85%EB%A5%98.md)                                                        |  



# Shortest-Job-First
---
- 각 프로세스의 다음 번 CPU burst time 을 가지고 스케줄링에 활용
- CPU burst Time 이 가장 짧은 프로세스를 먼저 스케줄

# Shortest-Remaning-Time-First
---
현재 실행 중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU를 빼앗김

# SJF is optimal
---
주어진 프로세스들에 대해 minimum average waiting time 을 보장. waiting time 이므로 preemptive 버전인 SRTF 일 때 optimal 함

waiting time 은 중간에 빼앗겨서 쉴 때도 포함.

# 문제점
---
- Long Process 가 Starvation 될 수 있음
- 다음 번 Cpu Burst time 을 어떻게 알 수 있는가?
	- 추정만이 가능
		- 과거의 CPU burst time을 이용해서 추정(exponential averaging)


# 관련 링크
---

# 출처
---