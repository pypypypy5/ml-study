---
{"dg-publish":true,"permalink":"///eigenvector/"}
---


![image.png](attachment:741cbda0-765e-4902-82b5-1fcbb484d5bf:image.png)

선형변환을 해도 크기만 변하는 벡터. 이게 강력한 이유는, 기저를 고유벡터들로 변환 (eigenbasis) 해두면 이후 원래 선형변환을 할때 복잡한 전단, 회전, 등이 아니라 단순 스칼라 곱의 stretch로 해석되기 때문이다. 복잡한 선형변환을 100번 한 후 결과를 봐야 한다면, 직접 그걸 하나하나 다 하는게 아니라 eigenbasis로 변환 후 stretch 100번 하고, 다시 원래 기저로 되돌리면 된다.