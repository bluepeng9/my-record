|               |                       |
|:--------------|:----------------------|
|  작성일          |  2023-04-11  |
|    분류         | [CPU](CPU.md)                       |

각 프로그램마다 CPU 버스트와 I/O 버스트가 차지하는 비율이 균일하지 않다. 어떤 프로세스는 I/O 버스트가 빈번해 CPU 버스트가 매우 짧은 반면, 어떤 프로세스는 I/O를 거의 하지 않아 CPU 버스트가 매우 길게 나타난다. 이와 같은 기준에서 프로세스를 크게 I/O 바운드 프로세스와 CPU 바운드 프로세스로 나눌 수 있다.

# CPU burst
---
프로세스 내에서 `CPU 명령`작업이 연속된 작업을 의미

# I/O burst
---
로컬 혹은 네트워크등의 I/O wait 작업이 연속되는것을 의미

# CPU bound job
---
CPU burst 시간이 긴 작업들이다. 보통 계산 작업 등이며 소수이다.

# I/o bound job
---
- 주로 사람하고 상호 작용하는 프로그램이 CPU burst, I/O burst 를 자주 반복한다. 
- CPU 를 사용하는 시간이 대체적으로 짧다. CPU로 계산하는 시간보다 I/O에 많은 시간이 필요하다.
- 다수의 프로그램이 해당
- 잠깐만 CPU 를 주면 I/O 작업을 할 수 있다.

# 관련 링크
---


# 출처
---
[4. 이화여자대학교 :: CORE Campus (ewha.ac.kr)](https://core.ewha.ac.kr/publicview/C0101020140325134428879622?vmode=f)
[5. CPU Bound vs I/O Bound (taes-k.github.io)](https://taes-k.github.io/2021/06/05/cpu-io-bound/)
[5. \[반효경 운영체제\] CPU Scheduling 1 (tistory.com)](https://steady-coding.tistory.com/530)