---
{"dg-publish":true,"permalink":"/js/promise/"}
---

**js promise**

promise로 비동기 객체 반환, 그동안 뒤에 코드가 실행된다. promise가 fullfilled나 rejected하면 .then이 마이크로태스크 큐에 들어가고, [[기초 cs/call stack\|call stack]] 다 비워지면 그제야 마이크로태스크 큐 비운다.

- **async 함수 안은 `await`에서 쪼개지고, 밖의 코드는 그냥 자기 순서대로 돈다.**
    
    그리고 나중에 “**`await`** 뒤 코드”가 _후속 microtask_로 붙는 것.