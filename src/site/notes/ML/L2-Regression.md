---
{"dg-publish":true,"permalink":"/ml/l2-regression/"}
---

$\approx$ Weight Decay
$$J(w) = \underbrace{\sum_{i=1}^{n} (y_i - \hat{y}_i)^2}_{\text{Loss (MSE)}} + \underbrace{\lambda \sum_{j=1}^{p} w_j^2}_{\text{Penalty (L2 Regularization)}}$$
# 문제
[[ML/Linear Regression\|Linear Regression]]에서 기존 [[확률-통계/MSE\|MSE]]의 [[Multicollinearity\|Multicollinearity]] 문제.
입력 변수(Feature)들끼리 상관관계가 너무 높으면, 모델은 어떤 변수가 결과(y)에 영향을 미쳤는지 구분하지 못합니다. 이로 인해 가중치($w$)의 조합이 무수히 많아지고, 특정 가중치가 **비상식적으로 커지는(Exploding)** 현상이 발생합니다.
$$w = (X^T X)^{-1} X^T y$$의 X에서 feature들에 해당하는 열 벡터들이 서로 거의 평행해지면서, xTx가 의 어느 고유값이 0에 가까워짐 -> 역행렬의 고유값은 반대로 폭발.
# 해결
가중치가 지나치게 커지지 않도록 패널티를 주는 것.