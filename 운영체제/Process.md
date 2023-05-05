|               |                       |
|:--------------|:----------------------|
|  작성일          |  2023-04-09  |
|    분류         |         [운영체제](%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C.md)              |

# Index
---
- [Process Control Block (PCB)](Process%20Control%20Block%20(PCB).md)
- [프로세스를  스케줄링하기 위한 큐](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EB%A5%BC%20%20%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81%ED%95%98%EA%B8%B0%20%EC%9C%84%ED%95%9C%20%ED%81%90.md)
- [스케줄러](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC.md)
- [프로세스의 상태](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%9D%98%20%EC%83%81%ED%83%9C.md)
- [프로세스 생성](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%20%EC%83%9D%EC%84%B1.md)
- [프로세스 종료](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%20%EC%A2%85%EB%A3%8C.md)
- [프로세스와 관련된 System Call](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80%20%EA%B4%80%EB%A0%A8%EB%90%9C%20System%20Call.md)
- [프로세스 간 협력](%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%20%EA%B0%84%20%ED%98%91%EB%A0%A5.md)

# 개념
---
프로세스란, 실행 중인 프로그램을 의미한다. 실행이 되면 그 프로세스만의 독자적인 주소 공간을 형성한다(code, data, stack). 프로세스가 실행되면 CPU 의 PC 레지스터가 code의 어느 부분을 가리키고 있다. 매 순간 code에서 Instruction 을 읽어서 CPU 의 레지스터에 값을 저장한다. 

# 프로세스 문맥(Context)
---
특정시점을 놓고 봤을 때, 이 프로세스가 어디까지 수행했는지 상태를 나타낸다. 
현재 시점의 프로세스의 문맥을 나타내기 위해서는 Program Counter 가 Code의 어느 부분을 나타내고 있는지, Process 의 메모리에 어떤 내용을 담고 있는 지 모두를 알아야 함. 이러한 모든 요소를 프로세스 문맥이라고 한다.

세 가지로 설명할 수 있다.
- CPU 의 수행상태를 나타내는 하드웨어 문맥
	- Program Counter
	- 각종 Register
- 프로세스의 주소공간
	- Code, Data, Stack
- 프로세스 관련 커널 자료 구조
	- PCB (Process Control Block)
	- Kernel Stack

# 프로세스의 특성 분류
---
프로세스는 그 특성에 따라 다음 두 가지로 나눔

## I/O-bound process
---
- CPU 를 잡고 계산하는 시간 보다 I/O에 많은 시간이 필요한 job
- many short cpu burst

## CPU-bound process
---
- 계산 위주의 job
- few very long CPU bursts


# 관련 링크
---
[CPU](CPU.md)
[커널 주소 공간의 내용](%EC%BB%A4%EB%84%90%20%EC%A3%BC%EC%86%8C%20%EA%B3%B5%EA%B0%84%EC%9D%98%20%EB%82%B4%EC%9A%A9.md)
[Thread](Thread.md)


# 출처
---
[7. 이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140318134023355997?vmode=f)