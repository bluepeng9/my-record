- 작성일: 2023-06-08
- 태그: 
- 분류
    - [스케줄러 종류](스케줄러%20종류.md)
- 관련 노트

---

- Ready Queue 를 여러 개로 분할한다.
    - `foreground` (interactive)
    - `background` (batch - no human interaction)
        - 사람과 interaction 없이 cpu 만 오랫동안 사용하는 등의 일
- 각 큐는 독립적인 스케줄링 알고리즘을 가진다.
    - `foreground` 
        - 응답시간을 짧게 유지해야 함
            - `Round Robin`
    - `background` 
        - context switch overhead를 줄여야 함
            - `FCFS`
- 어느 줄에 CPU 를 줄 것인지 결정해야 함
    - Fixed priority scheduling
        - 고정된 우선순위 스케줄링
        - starvation 이 발생할 수 있음
    - Time slice
        - 각 큐에 CPU time 을 적당한 비율로 할당
        - e.g.
            - 80% 는 `foreground`, 20% 는 `background`

---

# Reference

- [이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140401134252676046?vmode=f)