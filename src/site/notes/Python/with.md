---
{"dg-publish":true,"permalink":"/python/with/"}
---

[[context manager\|context manager]]를 사용하는 문법
__enter __: with 블록 안에 들어갈때 호출

__exit __: with 블록 나올때 호출

ex.

```jsx
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

블록 안에서 파일 사용, 블록 나가면 file.close() 자동 호출

→ 자원 관리에 많이 쓰인다.