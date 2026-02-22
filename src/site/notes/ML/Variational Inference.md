---
{"dg-publish":true,"permalink":"/ml/variational-inference/"}
---

[[ML/Gen Model/VAE\|VAE]], [[ML/BNN\|BNN]]과 같이 실제 분포를 바로 구하는 것이 어려울때 사용하는 방법.
# 방법
실제 분포를 근사하기 위해 아는 분포를 가져온다. [[확률-통계/Gaussian Distribution\|Gaussian Distribution]]과 같이. 
실제 분포와 가짜 분포 사이의 거리를 최소화하는 것이 학습의 목표가 되며, 다르게 말하면 [[ELBO\|ELBO]]의 최대화이다. 
$$\mathcal{L}(\phi) = \underbrace{\mathbb{E}_{q_\phi(w)}[\log P(D|w)]}_{\text{Likelihood (데이터 적합)}} - \underbrace{KL[q_\phi(w) || P(w)]}_{\text{Complexity (사전 지식과의 일치)}} $$
[[ML/general/reparametrization trick\|reparametrization trick]]이랑 많이 나온다. 