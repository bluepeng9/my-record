|               |                       |
|:--------------|:----------------------|
|  작성일          |  2023-04-12  |
|    분류         |  [스케줄러 종류](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC%20%EC%A2%85%EB%A5%98.md)                     |

Preemptive 스케줄러.

각 프로세스는 동일한 크기의 할당시간을 가짐(time quantum)을 가짐

- 할당 시간이 지나면 프로세스는 CPU를 빼앗기고(preempted) ready queue의 제일 뒤로 가서 다시 줄을 선다.
- n 개의 프로세스가 ready queue 에 있고 할당 시간이 q time unit 인 경우 각 프로세스는 최대 q time unit 단위로 CPU 시간의 1/n 을 얻는다.
	- 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.
 
# 성능
---
- q 를 크게 하면 FCFS와 같은 알고리즘이 됨
- q 를 작게 하면 context switch 오버헤드가 커진다

일반적으로 SJF 보다 average turnaround time 이 길지만 response time 은 더 짧다
- 만약 CPU 사용시간이 동일한 프로그램이 있을 때, 어느하나 먼저 끝나지 않아서 프로그램이 끝나는 시점이 멀어짐
- 하지만 일반적으로 긴 프로그램과 짧은 프로그램이 섞여있기 때문에 Round Robin이 효과를 발휘한다.

# 관련 링크
---
[First-Come First-Served](First-Come%20First-Served.md)
[스케줄링 성능 척도](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81%20%EC%84%B1%EB%8A%A5%20%EC%B2%99%EB%8F%84.md)

# 출처
---
q를