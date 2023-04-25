|                 |                         |
|:----------------|:------------------------|
|   작성일           |   2023-04-21   |
|     분류          |                         |
| 태그              | #데이터베이스                         |  

자바에서 database에 접속할 수 있도록 하는 api 입니다.

이들의 컨셉은 java application 에서 DBMS의 종류에 상관 없이 하나의 JDBC API 를 이용해 DB 작업을 처리하는 것입니다.

각각의 DMBS 는 이를 구현한 JDBC 드라이버를 제공합니다.

# 단점
---
- 간단한 SQL 을 실행하는 데도 중복된 코드를 반복적으로 사용해야 합니다.
- DB에 따라 일관성 없는 정보를 가진 채로 Checked Exception (SQLException) 처리를 해야 합니다.
- Connection 과 같은 공유 자원을 제대로 Release 해주지 않으면 시스템의 자원이 바닥나는 버그가 발생합니다.

# 출처
---
- [18. [10분 테코톡] ⏰ 아마찌의 ORM vs SQL Mapper vs JDBC - YouTube](https://www.youtube.com/watch?v=VTqqZSuSdOk&t=47s)

# 관련 링크
---