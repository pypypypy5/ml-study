---
{"dg-publish":true,"permalink":"/ml/theory/out-of-distribution/"}
---

### OOD 일반화

out-of-distribution. 지금 ai는 고차원 공간에서 학습 데이터가 몰려있는 [[수학/해석학/manifold\|manifold]]를 학습하고, 그 manifold 주변이라면 새로운 입력이 들어와도 훌륭하게 근사, 예측. 그러나 학습 데이터에서 벗어나면 실패. 근본 생성 원리를 파악한게 아니라 단순 표면적인 통계적 상관관계만 이해했기 때문

→ 단순히 데이터를 바탕으로 통계적 예측을 수행하는 것이 아니라 데이터가 생성된 근본적 원리를 학습, 담는 모델을 만들어야 한다.