---
{"dg-publish":true,"permalink":"/python/thread/"}
---

코어 하나면 한번에 하나의 스레드만 돌아가고 있는 것. 
코어 여러개면 프로세스 하나가 코어 여러개를 점유, 스레드 여러개가 동시에 병렬로 여러 코어에서 돌아갈 수 있음. 

[[Python/Python\|Python]]은 여러 코어인 상태에서도 [[Python/GIL\|GIL]]이 있으니 [[Python/GIL\|GIL]] 가진 스레드 이외의 다른 스레드들이 점유한 코어가 놀고 있는 것.