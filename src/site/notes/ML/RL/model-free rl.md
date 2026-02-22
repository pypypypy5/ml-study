---
{"dg-publish":true,"permalink":"/ml/rl/model-free-rl/"}
---

# 정의
[[ML/RL/model-based rl\|model-based rl]]의 문제를 해결하고자 model은 데이터 생성기로만 사용

# 방법론
### [[ML/RL/policy gradient\|policy gradient]]

모델은 단순히 합성 데이터 생성기로만 사용하기.

### [[ML/RL/dyna\|dyna]]

실제 데이터 + 합성 데이터로 학습하기.

실제 데이터로 모델 학습시키고, 모델에서 만든 학습데이터를 실제 데이터와 섞어서 q-learning과 같은 방식으로 학습 돌리기.

### [[ML/RL/MBPO\|MBPO]]

합성 데이터의 궤적이 길어질수록 오차는 그에 비례해서 증가

→ 실제 데이터로 앞부분, 그 뒤 몇 step만 model로 상상해서 합성 데이터 만들자

### [[Successor Representation\|Successor Representation]] (SR)

아예 이어지는 시퀀스를 value로 쓰는게 아니라 이후에 나오는 state들의 비율을 생각하기.

현재 정책을 유지하면 미래에 어떤 state들에 놓여있을지 비율을 구하고, reward를 곱해서 그걸 [[ML/RL/value function\|value function]]으로.

→ 상태 전이의 양상은 동일한데, reward만 바꾸면 변경이 가능하다.