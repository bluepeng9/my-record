- 작성일: 2023-04-09
- 태그: 
- 분류
    - [Thread](Thread.md)
- 관련 노트
    - [Context Switch](Context%20Switch.md)

---

# 응답 시간이 빨라진다

하나의 Process 안에 여러 개의 Thread 를 두게 되면, Thread 하나가 block 된 상태일 때, 다른 Thread 가 CPU 를 잡고 running 을 할 수 있습니다.

다음은 웹 브라우저를 사용한 예시입니다.

1. 네트워크를 통해 HTML 파일을 가져옵니다.
2. 여러 개의 Thread 를 사용해 하나의 Thread 가 이미지를 불러와 Blocked 되어 있을 때 다른 Thread 가 화면을 표시합니다.

---
# 메모리 및 자원의 효율성

동일한 일을 수행하는 걸 별도의 Process 를 만들면 메모리나 자원의 낭비가 됨. 독자적인 주소공간이 만들어져야 하고 주소공간은 메모리를 차지 하기 때문.

---
# 병렬성을 높일 수 있음

CPU 가 여러 개 있다면 1000 * 1000 행렬을 곱할 때 각각의 행 과 열을 곱하는 것을 서로 다른 CPU 가 실행

---
# Economy

프로세스를 만드는 것은 overhead가 크지만, Thread는 그렇지 않음. context switch 역시 마찬가지

---

# Reference

- [이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140321143516139010?vmode=f)