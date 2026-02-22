---
{"dg-publish":true,"permalink":"/ml/cross-entropy-loss/"}
---

# 정의
[[정보 이론/Cross Entropy\|Cross Entropy]]를 이용한 loss.
존재하는 모든 데이터에 대해, 진짜 분포를 가장 잘 (효율적으로) 설명하는 모델이 되도록 맞추는 것.

# ml이 [[확률-통계/MLE\|MLE]]인 이유
$$MLE=∑_ilogp_θ(y_i∣x_i)$$
$$CE loss = −∑_ilogp_θ(y_i∣x_i)$$
로, ce loss를 최소화하는 gradient descent는 결국 mle와 수학적으로 동일하다. 