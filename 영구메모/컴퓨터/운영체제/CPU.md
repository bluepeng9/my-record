|             |                     |
|:------------|:--------------------|
| 작성일         | 2023-04-08 |
|   분류        |       [[컴퓨터 시스템 구조 및 프로그램 실행]]              |

# Index
---
[[CPU-burst time 의 분포]]
[[CPU Scheduler & dispatcher]]

# 개념
---
PC(Program Counter)가 가리키는 부분을 Clock cycle 마다 실행 함.
CPU가 직접 접근하려면 Byte 단위로 접근이 가능한 매체여야 함 (ex. DRAM)

다음과 같은 요소가 있음
# Register
메모리 보다 빠르면서 정보를 저장할 수 있는 작은 공간
# mode bit
CPU 에서 실행되는 것이 운영체제인지, 사용자 프로그램인지 구분하기 위해 사용

Mode bit 를 통해 하드웨어 적으로 두 가지 모드의 operation 을 지원한다.
- 1 : 사용자 모드, 사용자 프로그램 수행
	- 사용자 프로그램에게 CPU 를 넘기기 전에 mode bit 를 1 로 세팅한다.
	- 제한된 Instruction 만 실행 가능
- 0 : 모니터 모드(커널 모드, 시스템 모드) , OS 코드 수행
	- 보안을 해칠 수 있는 중요한 명령어는 모니터 모드에서만 실행 가능하다.
	- Interupt / Exception 발생 시 하드웨어가 mode bit 를 0 으로 바꾼다.

# Interrupt line
CPU 는 Memory 에 있는 Instruction 을 실행하고 다음 번에 실행할 기계어의 주솟값이 증가. 이를 반복하는데, 키보드에서 값이 들어오거나 전에 디스크에 요청 했던 작업이 끝났다라는 것을 알기 위해 사용


# 관련 링크
---
[[Direct Memory Access]]

# 출처
---
[7. 운영체제 - 이화여자대학교 | KOCW 공개 강의](http://www.kocw.net/home/search/kemView.do?kemId=1046323)