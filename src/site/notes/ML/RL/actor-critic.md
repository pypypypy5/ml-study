---
{"dg-publish":true,"permalink":"/ml/rl/actor-critic/"}
---



기존에 policy gradient를 위해 쓰이던 REINFORCE는 끝까지 다 가보고 한번에 업데이트, 때문에 중간에 잘못된 행동이나 운빨로 된 것들도 강화됨.

→ 가치 함수 도입해서 각 action들 하나하나를 제대로 평가하자

## 원리

critic이 가치 함수로서 해당 s,a에 대한 가치함수의 값을 예측하고, actor가 critic이 낸 v의 값을 loss처럼 사용하여 학습한다. 이때 critic 또한 예측한 값을 이후에 실제 나오는 보상들을 바탕으로 계산된 실제 가치와 비교하여 더 정확한 v를 내도록 학습한다.

