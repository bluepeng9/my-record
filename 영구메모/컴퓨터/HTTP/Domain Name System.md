- 작성일: 2023-04-30
- 태그: #작성중 
- 분류:
	- [HTTP](HTTP.md)
- 관련 노트:
---

```
+-----------------+     +-----------------+     +-----------------+
|                 |     |                 |     |                 |
|  DNS Resolver   |     | Root Nameserver |     |  TLD Nameserver |
|                 |     |                 |     |                 |
+-----------------+     +-----------------+     +-----------------+
       ^                      ^                      ^
       |                      |                      |
       +----------------------+----------------------+
       |                      |
       |                      |
       v                      v
+-----------------+     +-----------------+
|                 |     |                 |
|    Web Browser  |     |Authoritative NS |
|                 |     |                 |
+-----------------+     +-----------------+
```

| 도메인명       | IP            |
|:-----------|:--------------|
| google.com | 200.200.200.2 |
| aaa.com    | 210.210.210.3 |  

1. 도메인 명으로 접근
2. IP로 응답
3. 접근

---
# 필요성

IP는 기억하기 어렵기 때문에, 이름을 `IP`로 변환해주는 서비스가 필요합니다.

---

# 기능

## Hostname to IP address translation (A, AAAA)

`Hostname`을 `IP`주소로 변환해 줍니다.

`A`는 `IPV4` 주소를 의미합니다.

`AAAA`는 `IPV6` 주소를 의미합니다.

## Host aliasing

복잡한 호스트 네임을 가진 호스트는 하나이상의 별명을 가질 수 있다. 이때 복잡하지만 실제 지정한 호스트 네임을 정식 호스트 네임(Canonical hostname)라고 하며 기억하기 쉽게 사용되는 별명들을 별칭 호스트 네임이라고 한다. DNS는 호스트의 IP주소뿐만 아니라 제시한 별칭 호스트 네임에 대한 정식 호스트 네임을 얻기 위해 이용될 수 있다.

- alias name
	- `naver.com`과 같이 기억하기 쉬운 주소
- canonical name
	- `alias name`의 진짜 host name
	- ex) www.naver.com.nheos.com
 

## Mail server aliasing

`@naver.com`으로 메일을 보내면, `naver.com`의 이름을 갖는 컴퓨터가 받는 것이 아니라, `naver.com`을 서비스하는 사업자의 메일 서버로 메일이 전달됩니다.

마찬가지로 메일 서버의 주소를 다 외울 수는 없으니 `naver.com`과 같은 짧은 별칭을 두어 편리하게 이용할 수 있도록 합니다.


## Load distribution

```
Example of Round-Robin Load-Balancing when a request
is sent to naver.com:
Servers: A(mx1.naver.com), B(mx2.naver.com), C(mx3.naver.com)
A: 1st, 4th, 7th
B: 2nd, 5th, 8th
C: 3rd, 6th, 9th
DNS Requests: 1, 2, 3, 4, 5, 6, 7, 8, 9

1 -> A
2 -> B
3 -> C
4 -> A
5 -> B
6 -> C
7 -> A
8 -> B
9 -> C
```

요청에 따라 다른 응답을 주어 서버 부하를 줄일 수 있습니다.

---
# Reference

- James F. Kurose and Keith W. Ross, _Computer Networking A Top-Down Approach_, 7th Edition, Pearson, 2016.
- [What is DNS-based load balancing? | DNS load balancing | Cloudflare](https://www.cloudflare.com/learning/performance/what-is-dns-load-balancing/)

---