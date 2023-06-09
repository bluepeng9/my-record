- 작성일: 2023-06-08
- 태그: 
- 분류
    - [운영체제](운영체제.md)
- 관련 노트
    - [Context Switch](Context%20Switch.md)

---

- OS 는 타이머를 설정해 일정 기간 뒤 `Interrupt` 를 만듭니다.
- OS 는 application 을 프로세서에 할당합니다.
- 타이머가 `expire` 되면, `timer interrupt` 를 발생시킵니다.
- 프로세서는 `timer interrupt handler` 로 jump 합니다.
- 스케줄러는 다음 프로세스를 선택합니다.

---

# Reference

- moca - Time sharing and context switching