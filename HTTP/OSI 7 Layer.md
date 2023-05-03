- 작성일: 2023-04-30
- 태그: 
- 분류:
	- [HTTP](HTTP.md)
- 관련 노트:
***
# Layers

| Layer | Name | Examples |
| --- | --- | --- |
| 7 | Application | HTTP, SMTP, FTP, TELNET |
| 6 | Presentation | SSL, ASCII |
| 5 | Session | NetBIOS, RPC, WinSock |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, ICMP, IGMP |
| 2 | Data link | Ethernet, HDLC, PPP |
| 1 | Physical | RS-232, X.25, DSL |

## Application

>supporting network application

END 유저에게 서비스를 제공하기 위한 계층

## Presentation

>allow applications to interpret meaning of data, e.g., encryption, compression, machine-specific conventions

application이 어떻게 data를 해석할 것인지 명세한 계층

## Session

> synchronization, checkpointing, recovery of data exchange 

End와 End 사이 Connection을 맺고 중간에 끊어주고, 다시 복구하는 것들을 정의한 계층

## Transport

> process-process data transfer

Application과 Netwrok계층 사이에 데이터 교환이 정상적으로 이루어지고 있는지 확인하는 계층

## Network

> routing of datagram from source to destination

클라이언트가 보낸 패킷을 라우터가 어떻게 처리할 것인지 결정하는 계층

## Link

>data transfer between neighboring network elements

라우터 하나하나 링크 단위로 연결을 책임지는 계층

## Physical Layer

> bits "on the wire"

매체에 신호를 어떻게 보낼 것인가 책임지는 계층

---
# OSI, TCP/IP Protocol

- Application, Presentation, Session 레이어들이 TCP/IP Protocol 에서는 Application layer 하나로 mapping 되었다.



***
# Reference
- James F. Kurose and Keith W. Ross, _Computer Networking A Top-Down Approach_, 7th Edition, Pearson, 2016.

***