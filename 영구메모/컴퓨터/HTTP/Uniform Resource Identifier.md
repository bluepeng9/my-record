- 작성일: 2023-05-01
- 태그: 
- 분류
	- [HTTP](HTTP.md)
- 관련 노트
---

```
URI: Uniform Resource Identifier
  |
  |-- URL: Uniform Resource Locator
  |     |
  |     |-- Scheme: Protocol
  |     |     (e.g. http, https, ftp, mailto)
  |     | 
  |     |              |-- Domain: the server hosting the resource
  |     |-- Authority--|     (e.g. www.google.com)
  |     |              |-- Port: Protocol port
  |     |                    (e.g. 80, 443)
  |     |
  |     |-- Path: Path to resource
  |     |     (e.g. /index.html)
  |     |-- Parameters: Extra info
  |     |     (e.g. ?q=hello&hl=ko)
  |     |-- Anchor: Part in resource. Also called fragment
  |           (e.g. #section1)
  |
  |-- URN: Uniform Resource Name
        |
        |-- Scheme: urn
        |-- Namespace Identifier: Namespace
        |     (e.g. isbn, doi, uuid)
        |-- Namespace Specific String: ID in namespace
              (e.g. 0451450523)

```

---
# URI란

간단히 말해 리소스를 식별하는 문자열로, URL과 URN으로 분류할 수 있습니다.

- URL
	- Location으로 리소스를 식별합니다.
		- e.g. 집의 주소
		- 위치는 변할 수 있습니다.
- URN
	- Name으로 리소스를 식별합니다.
		- e.g. 도서의 isbn 번호
		- 이름은 변하지 않습니다.

---
# Reference

- [URL, URI, URN: What's the Difference? (auth0.com)](https://auth0.com/blog/url-uri-urn-differences/)
- [모든 개발자를 위한 HTTP 웹 기본 지식 - 인프런 | 강의 (inflearn.com)](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)