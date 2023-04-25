|             |                     |
|:------------|:--------------------|
| 작성일         | 2023-04-08 |
|   분류        |       [[운영체제]]              |

마이크로프로세서(CPU)가 프로그램을 실행하고있을 때, 입출력하드웨어 등의 장치에 예외상황이 발생하여 처리가 필요할 경우에 CPU 에게 알려 처리할 수 있도록 하는 것을 말한다.

CPU가 Interrupt를 당하면, Interrupt 를 당한 시점의 레지스터와 program counter 를 save 한 후 CPU 의 제어를 인터럽트 처리 루틴에 넘긴다.

### 넓은 의미의 Interrupt
- Interrupt (하드웨어 인터럽트): 하드웨어가 발생시킨 인터럽트
- Trap (소프트웨어 인터럽트)
	- Exception: 프로그램이 오류를 범한 경우
	- System Call: 프로그램이 커널 함수를 호출하는 경우
 
### 인터럽트 관련 용어
- 인터럽트 벡터
	- 해당 인터럽트의 처리 루틴 주소를 가지고 있음
 
- 인터럽트 처리 루틴(= Interrupt Service Routine, 인터럽트 핸들러)
	- 해당 인터럽트를 처리하는 커널 함수

# 처리 과정
---
1.  실행중인 프로그램을 중단.
2.  현재 프로그램 상태를 보관. (Context switching)
3.  Interrupt 처리 루틴을 실행.
4.  Interrupt 서비스 루틴을 실행.
5.  Interrupt 요청 신호가 발생했을 때 보관한 PC의 값을 복원하여 이전 실행 위치로 복귀.
6.  이어서 프로그램을 진행.

# 관련 링크
---


# 출처
---
- [16. 2023-CS-Study/os_interrupt.md at main · Fancy96/2023-CS-Study · GitHub](https://github.com/Fancy96/2023-CS-Study/blob/main/OS/os_interrupt.md)
- [8. 인터럽트 - 위키백과, 우리 모두의 백과사전 (wikipedia.org)](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8)