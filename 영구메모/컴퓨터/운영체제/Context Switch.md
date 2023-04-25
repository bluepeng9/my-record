|              |                                                                                                                                                                                                                                          |
|:-------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   작성일        |                                                                                                                           2023-04-08                                                                                                     |
|    분류        |  [[Process]]                                                                                                                                                                                                                                   |

CPU를 한 프로세스에서 다른 프로세스로 넘겨주는 과정.

CPU 가 다른 프로세스에게 넘어갈 때 운영체제는 다음 과정을 수행한다.
- CPU 를 내어주는 프로세스의 상태를 그 프로세스의 PCB 에 저장
- CPU 를 새롭게 얻는 프로세스의 상태를 PCB 에서 읽어옴

# Context 란
---
>프로그래밍에서 Context는 (동작, 작업들의 집합)을 (정의, 관리, 실행)하도록 하는 (최소한의 상태, 재료, 속성)을 포함하는 (객체, 구조체, 정보)이다.  
[What exactly is context in programming?](https://www.quora.com/What-exactly-is-context-in-programming?no_redirect=1)


# 헷갈릴 수 있는 개념
---
## System Call 이나 Interrupt 발생 시 반드시 context switch 가 일어나는 것은 아님
사용자 프로세스 A 로부터 또 다른 사용자 프로세스 B로 넘어가는 것 Context Switch 라고 하기 때문

1. 사용자 프로세스 A > kernel mode > 사용자 프로세스 A
2. 사용자 프로세스 A > kernel mode > 사용자 프로세스 B (Context switch O)

1 의 경우에도 CPU 수행 정보 등 context 의 일부를 PCB 에 save 해야 하지만 문맥교환을 하는 2 의 경우 그 부담이 훨씬 큼 (eg. cache memory flush)

# Thread의 context switching
---

thread는 process와 다르게 thread 간에 공유하는 영역이 많기 때문에, thread의 context switching이 process의 context switching보다 빠르다.

thread는 각 thread간에 공유하는 데이터가 있기 때문에, cache 데이터가 유효하다. 그래서 cache 적중을 통해 더 빠른 context switching이 가능하다.


# 물음
---
Thread Context Switch 와 Process Context Switch 가 분리되어 있는 용어 같음.

# 관련 링크
---
[[Process Control Block (PCB)]]
[[Thread]]
[[Process]]

# 출처
---
[8. 이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140318134023355997?vmode=f)
[11. \[운영체제\] Context Switching (컨텍스트 스위칭) (velog.io)](https://velog.io/@kangdev/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-Context-Switching-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8-%EC%8A%A4%EC%9C%84%EC%B9%AD)
[13. Context Switching 이란? (velog.io)](https://velog.io/@curiosity806/Context-Switching%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-process%EC%99%80-thread)