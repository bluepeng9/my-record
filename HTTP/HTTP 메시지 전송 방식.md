- 작성일: 2023-05-04
- 태그: 
- 분류
    - [HTTP 메시지](HTTP%20메시지.md)
- 관련 노트
---

```
HTTP 메시지 전송방식
|
+-- 단순 전송
|
+-- 압축전송
|
+-- 분할 전송
|
+-- 범위 전송
```

HTTP 메시지 전송방식에 대해 알아보겠습니다.

---

# 단순 전송

```HTTP
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
```

- Content의 길이를 알려주고 단순히 전송합니다.

---

# 압축 전송

```HTTP
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Encoding: gzip
Content-Length: 521

lkj123kljoiasudlkjaweioluywlnfdo912u34ljko98udjkl
```

- 서버에서 데이터를 압축해 전달해줍니다.
- Content-Encoding을 통해 압축 방식을 알려줍니다.

---

# 분할 전송

```HTTP
HTTP/1.1 200 OK
Content-Type: text/plain
Transfer-Encoding: chunked

5
Hello
5
World
0
\r\n
```

1.  5바이트 Hello를 전송합니다.
2.  5바이트 World를 전송합니다.
3. 전송을 마칩니다.

특징은 다음과 같습니다.

- Content-Length를 사용할 수 없습니다.
    - 길이를 예상할 수 없기 때문입니다.

---

# 범위 전송

```
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Range: bytes 1001-2000 / 2000

qweqwe1l2iu3019u2oehj1987askjh3q98y
```

- 범위를 지정해 요청합니다.

---

# Reference

- 