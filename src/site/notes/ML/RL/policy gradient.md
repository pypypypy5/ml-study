---
{"dg-publish":true,"permalink":"/ml/rl/policy-gradient/"}
---


$$ V^{\pi}(\mathbf{s}) = E[Q^{\pi}(\mathbf{s}, \mathbf{a})] $$

위의 평균 q를 잡고, 특정 a의 q가 평균 q보다 높다면 그건 평균보다 우수한 a이므로 선택 확률을 높이고, 반대면 줄이기.

q-v를 보통 [[ML/RL/advantage\|advantage]]라고 부르며, 이 행동이 얼마나 특별히 더 좋은지를 나타내는 지표가 됨.

# 방법론
## [[ML/RL/REINFORCE\|REINFORCE]]