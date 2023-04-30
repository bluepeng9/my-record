|               |                       |
|:--------------|:----------------------|
|  작성일          |  2023-04-09  |
|    분류         |      [운영체제](운영체제.md)                 |

# Index
---
[Thread 사용의 장점](Thread%20%EC%82%AC%EC%9A%A9%EC%9D%98%20%EC%9E%A5%EC%A0%90.md)

# 개념
---
> A thread (or *lightweight process*) is a basic unit of CPU utilization

프로세스 내부에 CPU 수행 단위가 여러 개 있는 경우를 뜻 함. 프로세스 하나에 CPU 수행 단위만 여러 개 두고 있는 것을 Thread 라 부름.

Thread의 구성
- program counter
- register set
- stack space

Thread가 동료 Thread 와 공유하는 부분(=task)
- code section
- data section
- OS resources

# Kernel Thread
---
Thread가 여러 개 있다는 사실을 운영체제 커널이 알고 있음. 그래서 하나의 Thread 에서 다른 Thread로 CPU 가 넘어가는 것도 Kernel 이 Cpu Scheduling 하듯 넘겨 줌.

# User Thread
---
프로세스 안에 Thread 가 여러 개 있다는 사실을 운영체제는 모름. 유저 프로그램이 스스로 여러 개의 Thread 관리. 따라서 구현 상의 제약점이 있을 수 있음.

# 관련 링크
---
[Process Control Block (PCB)](Process%20Control%20Block%20(PCB).md)
[Process](Process.md)

# 출처
---