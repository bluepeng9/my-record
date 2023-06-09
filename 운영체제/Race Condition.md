- 작성일: 2023-06-08
- 태그: 
- 분류
    - [운영체제](운영체제.md)
- 관련 노트

---

# Kernel 수행 중 인터럽트 발생 시

- 커널 모드 running 중 interrupt 가 발생하여 인터럽트 처리루틴이 수행
    - 양쪽 다 커널 코드이므로 kernel address space 공유
- e.g.
    - count++ 작업 수행 중 interrupt 발생하여 count-- 를 수행하는 경우
    
---

# Context switch가 일어나는 경우

Process 가 System call 을 하여 Kernel mode로 수행 중인데 context switch 가 일어나는 경우

- 두 프로세스의 address space 간에는 data sharing 이 없습니다.
- 그러나 System call 을 하는 동안에는 kernel address space 의 data 를 access 하게 됩니다.
- 이 작업 중간에 CPU 를 preempt 해가면 race condition 이 발생하게 됩니다.
- e.g
    - kernel mode 에서 count++ 를 수행하고 있을 때, 할당된 시간이 끝나 다른 프로세스로 넘어갔을 경우

---

# Multiprocessor 에서 shared memory

- 한 번에 하나의 CPU 만이 커널에 들어갈 수 있게 합니다.
- 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 대한 lock / unlock 을 수행 합니다.

---

# Reference

- [이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140401134252676046?vmode=f)