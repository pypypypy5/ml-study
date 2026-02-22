---
{"dg-publish":true,"permalink":"/ml/rl/exploration/"}
---

<-> [[Exploitaion\|Exploitaion]]
# 정의
어쩌면 지금보다 나을지도 모르는 다른 방법들 탐색하기

[[regret\|regret]]: 최적의 방법을 처음부터 알았을때 얻을 수 있는 reward 총합 - 지금 방법으로 뽑아먹을 수 있는 reward의 총합

→ regret을 줄이는 것이 exploration의 목표

# 방법론

## optimism

지금까지 가본적 없는 곳에 가면 보너스 주기

r+B → r+

## posterior sampling

여러 경우의 수 중 하나가 잘될거라 믿고 끝까지 진행해보기

구현: 신경망의 출력 부분에 여러개의 헤드를 두고, 그 헤드들이 독립적으로 학습하도록 만들어둔다.

## information gain

이전에 경험했던 경로와 상당히 다른, 즉 새로운 정보를 얻을 수 있는 경로를 갔을때 보상을 주는 방식.

$IG(z, y | a) = \mathbb{E}_y [ \mathcal{H}(\hat{p}(z)) - \mathcal{H}(\hat{p}(z) | y) | a ]$ (결과 y, 알고자 하는 세계 정보 z)

z를 환경의 동역학 모델 파라미터인 theta라 한다면

$IG(\theta, y | a) = D_{KL}(p(\theta | h, y) \parallel p(\theta | h))$와 같이 [[정보 이론/KL-Divergence\|KL-Divergence]] 형태로 information gain이 표현된다.

### 구현:

### **VIME (Variational Information Maximizing Exploration)**

아예 사후 분포를 바로 계산하는 것은 어렵다.

→ 세계모델에 해당하는 [[ML/BNN\|BNN]] 따로 만들어서 새로 얻은 정보 의해 어떻게 파라미터가 변하는지를 보고 ig, 즉 이전과 이후의 kld를 계산하자.

vae와 유사한 문제, 유사한 솔루션. 여기서도 [[ELBO\|ELBO]] 사용한다. 그런데 bnn이 어떻게 동작하는지는 나중에 추가로 공부해야.

### Novelty-seeking via Errors

내가 가진 지식으로 예측하기 어려운 대상을 찾아다니도록 만들기.

구현:

해싱, ex2, rnd