- 작성일: 2023-04-30
- 태그: 
- 분류:
	- [TCP](TCP.md)
- 관련 노트:
	- [UDP segment 구조](UDP%20segment%20구조.md)
***

| Source Port | Destination Port |
|:-----------:|:----------------:|
| 16 bits     | 16 bits          |

| Sequence Number | Acknowledgment Number |
|:---------------:|:---------------------:|
| 32 bits         | 32 bits               |

| Data Offset | Reserved | U | A | P | R | S | F | Window Size |
|:-----------:|:--------:|:-:|:-:|:-:|:-:|:-:|:-:|:-----------:|
| 4 bits      | 6 bits   | 1 bit | 1 bit | 1 bit | 1 bit | 1 bit | 1 bit | 16 bits     |

| Checksum    | Urgent Pointer |
|:-----------:|:--------------:|
| 16 bits     | 16 bits        |

| Options |
|:-----------------:|
| variable length   |

| application data|
|:-----------------:|
| variable length   |


---
# Sequence Number

> Byte stream "number" of first byte in segment's data

- application data에 들어있는 첫 번째 byte
	- ex) Get /index.html HTTP ~~~ 일 때 G
 - 시작 값이 0이 아닌 랜덤 숫자
 - 시작 값이 아니라면 앞서 보냈던 Sequence Number + Application data의 길이

---
# Acknowledgment number

>Seq # of next byte expected from other side

- 상대방으로부터 받기를 기대하는 순서 number
	- ex) 만약 값이 1000 이라면, 나 999까지 받았으니 1000 받기를 희망해 라는 뜻
- cumulative ACK


***
# Reference

- James F. Kurose and Keith W. Ross, _Computer Networking A Top-Down Approach_, 7th Edition, Pearson, 2016.

***