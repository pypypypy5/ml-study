---
{"dg-publish":true,"permalink":"/ml/rl/q-learning/"}
---


현재 s를 받아 각 a에 대한 q ([[ML/RL/Q-function\|Q-function]] - action value function)을 출력. q가 가장 높은 action으로 진행하면 되는거.

[[ML/RL/bellman equation\|bellman equation]]을 활용하여,

**정답(Target) = (방금 얻은 실제 보상 $r$) + ($\gamma \times$ 다음 상태 $s'$에서 내가 받을 수 있는 가장 높은 Q-값)가 되는거고,**

이거에 맞도록 학습을 진행.

## 문제

### 샘플 사이 강한 상관관계

차 운전할때 몇백 프레임동안 비슷한 광경이 계속됨. 이러면 직진 상황에만 과도하게 몰입하게 되어 판단력을 잃는다. (샘플들이 iid를 만족하지 못함)

### 움직이는 과녁

정답 자체에 네트워크가 출력하는 q 값이 들어가있다. 그러니 정답과 아까 내 출력을 비교해서 학습하고 나면 다시 정답이 변하는 꼴.

→ 수렴성이 보장되지 않으며, 학습이 불안정하다.

## 해결

### [[ML/RL/replay buffer\|replay buffer]]

나온 (s,a,s’,r)을 바로 학습하는게 아니라 replay buffer에 넣어두고 섞어서 학습

→ 샘플 사이 시간적 상관관계가 깨진다. + batch process 가능

### 과녁 고정하기

매번 바로 바로 학습하며 네트워크 바꾸는게 아니라 나중에 한번에 몰아서 batch process.

→ 정답이 계속 변하지 않으며, 일반 dl에서 쓰는 mini batch, gd를 사용해 학습이 안정적으로 진행된다.

### [[ML/RL/double q-learning\|double q-learning]]

오차로 인해 실제보다 살짝 높은 가치를 가지고 있다고 판단한 것인데, 이게 계속 전파되면서 오차가 커지고 모델이 확증편향을 가지게 된다.

→ 실제 action 결정용 네트워크 하나, 점수만 판단하는 네트워크 하나 따로 둬서 action 네트워크가 오바하지 않도록 계속 검수한다.

## n-step

q learning과 같이 가치 함수 볼 때

1-step TD (Temporal difference)는 $R_{t+1}+γV(S_{t+1})$를 더한다.

n-step은 대신에 $R_{t+1}+γR_{t+2}+⋯+γ^{n−1}R_{t+n}+γ^nV(S_{t+n})$ 하는 식으로 더 이후의 실제 보상을 보는 방식.