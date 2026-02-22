---
{"dg-publish":true,"permalink":"/python/yield/"}
---

값을 return하는건데, return과 달리 yield해도 함수 끝나는게 아니라 이후로 계속됨. yield 쓴 함수는 [[Python/제너레이터\|제너레이터]] 객체가 되며, 함수 밖에서는 next()를 통해 하나씩 받아 올 수 있다.

ex.

```jsx
def gen():
    yield 1
    yield 2
    yield 3

g = gen()
print(next(g))  # 1
print(next(g))  # 2
print(next(g))  # 3
```
