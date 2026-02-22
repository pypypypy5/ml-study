---
{"dg-publish":true,"permalink":"/ml/rl/m-hc/"}
---

[https://gemini.google.com/share/09ee34831bb6](https://gemini.google.com/share/09ee34831bb6)

# [[ML/general/hyper connection\|hyper connection]]


# manifold constrained HC

$h_t = f_t\left( \mathcal{P} \left( \sum_{i=1}^{t-1} w_{ti} h_i \right) \right)$

w는 직교 행렬, p는 projection 행렬

## 기본 아이디어

먼저 각 h를 w를 통해 안정적인 [[수학/해석학/manifold\|manifold]]로 올리고, 이게 다 합쳐질때 manifold에 벗어날 수 있으니 p를 통해 다시 manifold 위에 올린다.

→ 신호들을 manifold 위에 올려서 합쳐졌을때 너무 커지지 않도록 한다.

## 신호 정보 보존

### [[수학/선형대수/subspace coding\|subspace coding]]
을 이용해 각 레이어들의 정보를 안정적으로 합친다.

### [[수학/해석학/stiefel manifold\|stiefel manifold]]

w들이 학습되며 변형될때 w_i, w_j가 서로 겹치지 않고 서로 직교성이 유지되도록 제약 조건으로 이 manifold 위에 있도록 한다.

### [[수학/선형대수/projection matrix\|projection matrix]]

wh를 모두 더하면 그래도 manifold에서 나갈 수 있다. 때문에 마지막으로 manifold에 투영하는 P를 거쳐 manifold 위에 있도록 고정.

## 신호 세기 분배

그냥 전부 더하고 바로 연결하면 신호 너무 커진다.

이전 레이어가 다음 레이어에 얼마나 강한 신호를 보낼지를 정하는 것.

### [[수학/선형대수/doubly stochastic matrix\|doubly stochastic matrix]]

1. **비음수성 ($A_{ij} \ge 0$):** 모든 원소가 0 또는 양수여야 합니다.
2. **행의 합이 1:** 각 가로줄(Row)의 원소들을 다 더하면 1이 됩니다.
3. **열의 합이 1:** 각 세로줄(Column)의 원소들을 다 더하면 1이 됩니다.

→ 각 레이어가 다른 레이어에 얼마나 강하게 보낼지를 나타냄. 합이 1

→ 레이어가 받는 신호의 크기의 총합이 일정하게 제한. 합이 1

각 세기 파라미터를 학습가능한 파라미터로 둬서 어디에 얼마나 강하게 보내야 하는지를 모델이 학습하게 한다.

정규화를 유지하기 위해 [[수학/선형대수/sinkhorn-knopp argorithm\|sinkhorn-knopp argorithm]]을 사용.

## 해결

1. 이전 레이어들에서 필요 정보만 추출해서 저장
2. 이전 레이어들의 정보를 압축해서 저장

$h_t = f_t\left( \mathcal{P} \left( \sum_{i=1}^{t-1} w_{ti} h_i \right) \right)$ $(\alpha^2 + \beta^2 \approx 1)$