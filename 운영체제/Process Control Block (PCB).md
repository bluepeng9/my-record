- 작성일: 2023-04-09
- 태그: 
- 분류
    - [Process](Process.md)
- 관련 노트
    - [Context Switch](Context%20Switch.md)

---

![Pasted image 20230409123330](%EC%B2%A8%EB%B6%80%20%ED%8C%8C%EC%9D%BC/Pasted%20image%2020230409123330.png)

---
# 개념 

- 특정 프로세스에 대한 중요한 정보를 저장하고 있는 운영체제의 자료구조입니다.
- 프로세스의 생성과 동시에 고유한 PCB 를 생성합니다.
    - 프로세스 관리 목적입니다.

---
# 구성 요소
- (1) OS가 관리 상 사용하는 정보
	- Processing State, Process ID
	- Scheduling information, Priority
- (2) CPU 수행 관련 하드웨어 값
	- Program Counter, Registers
- (3) 메모리 관련
	- Code, Data, Stack 의 위치 정보
- (4) 파일 관련
	- Open file descriptors

---
# Reference

- 