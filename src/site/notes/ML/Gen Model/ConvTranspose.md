---
{"dg-publish":true,"permalink":"/ml/gen-model/conv-transpose/"}
---

**ConvTranspose**

간단히 말해 conv의 전치, 역과정. 커널로 input을 읽고 총합하는게 아니라 커널의 각 element에 픽셀 하나를 element wise 곱하고 output에 넣는다. 겹치는 부분은 더한다.

[https://westlife0615.tistory.com/257](https://westlife0615.tistory.com/257)

**실무 팁**

1. encoder 결과로 평균은 평균 그대로 가져오지만, 표준편차는 logvar 형태로 내놓도록 학습시킨다.
    1. 분산은 양수여야 하는데 신경망이 음수 내놓으면 안되므로 조건 자동으로 충족하도록 log를 내놓도록 한다.
    2. 분산이 너무 작거나, 클 경우 신경망이 깔끔하게 내놓기 힘들다. 그래서 아예 log 취해 작은 경우, 큰 경우 모두 안정적으로 돌아가도록.
    3. 나중에 kl divergence loss 만들때는 logvar 형태로 하므로 log 취하며 값 뭉게지지 않도록 바로.