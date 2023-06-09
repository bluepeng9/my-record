- 작성일: 2023-04-11
- 태그: 
- 분류
    - [CPU](CPU.md)
- 관련 노트

---
# Index

- [스케줄링 성능 척도](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81%20%EC%84%B1%EB%8A%A5%20%EC%B2%99%EB%8F%84.md)
- [스케줄러 종류](%EC%8A%A4%EC%BC%80%EC%A4%84%EB%9F%AC%20%EC%A2%85%EB%A5%98.md)

---
# CPU Scheduler

스케줄러는 하드웨어일까? 어떤 것일까? 운영체제 안에 CPU 스케줄링을 하는 코드, 이 부분을 스케줄러 라고 부른다.

- Ready 상태의 프로세스 중 에서 이번에 CPU를 줄 프로세스를 고른다.

---
# dispatcher

- CPU 의 제어권을 CPU Scheduler에 의해 선택된 프로세스에게 넘긴다
- 이 과정을 Context switch 라고 한다

---
# CPU Scheduling 이 필요한 경우

프로세스에게 다음과 같은 상태 변화가 있을 때 필요하다.

1. Running -> Blocked
	- ex) I/O 요청하는 System Call
2. Running -> Ready
	- ex) 할당 시간 만료로 timer interrupt
3. Blocked -> Ready
	- ex) I/O 완료로 Interrupt
4. Terminate

1, 4에서의 스케줄링은 nonpreemptive (= 강제로 빼앗지 않고 자진 반납)
다른 스케줄링은 모두 preemptive (= 강제로 빼앗음)

---
# Reference