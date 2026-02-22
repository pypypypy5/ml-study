---
{"dg-publish":true,"permalink":"/ml/gen-model/vae/"}
---

[[ML/Gen Model/Auto Encoder\|Auto Encoder]]의 문제를 해결하여 [[ML/general/reparametrization trick\|reparametrization trick]]을 통해 z를 확률분포로 파악하기 쉽도록 했다.

# 해결
auto encoder의 문제를 latent space의 형태를 정규 분포로 만듦으로써 간단히 해결한다.

$$ logp_θ(x)=E_{q_ϕ}(z∣x)[logp_θ(x∣z)]−D_{KL}(q_ϕ(z∣x)∥p(z))+D_{KL}(q_ϕ(z∣x)∥p_θ(z∣x)) $$

KL Divergence는 항상 0 이상이므로,

$$ logp_θ(x)≥E_{q_ϕ}(z∣x)[logp_θ(x∣z)]−D_{KL}(q_ϕ(z∣x)∥p(z)) $$

가 성립하고, 이게 결국 최소화의 대상이 되는 ELBO (Evidence Lower BOund)가 되는 것이다.

ELBO, 즉 VAE의 loss는,

$$ L_{VAE}=−E_{q_ϕ}(z∣x)[logp_θ(x∣z)]+D_{KL}(q_ϕ(z∣x)∥p(z)) $$

여기서 p(z)는 prior로, 표준정규분포라고 생각한다. 그래서 뒤의 KL Divergence는 posterior가 prior인 p(z), 정규분포에서 멀어지는데 패널티를 주는 “KL regularization”다.

앞의 항은 decoder가 z에서 x를 얼마나 잘 복원하는지를 나타내는 “reconstruction loss”다.

1. likelihood를 계산하지 못하는 문제를, 진짜 posterior 대신 appoximate posterior를 사용함으로써 해결한다. ELBO는 계산 가능하기 때문.
2. latent space가 편중되는 문제를 kl term으로 조정, latent space를 올바른 구 모양으로 조정하여 어디에서 sample하더라도 정상적인 샘플이 나오도록 한다.

### 실무

vae - [[정보 이론/KL-Divergence\|KL-Divergence]] loss를 너무 크게 키우면 reconstruct 쪽이 역으로 눌려서 제대로된 학습이 안된다. 그래서 kld 앞에 beta라는 가중치를 조절해서 영향을 줄일 수 있다.

loss를 계산할때 batch size로 평균을 내서 규모를 맞춰야 하는데, 픽셀 수로 맞춰서 gradient vanish 가 나올 수 있다.

중요! - 하다가 안되면 그냥 바로 데이터, 실제 결과를 까보자. 이미 잘 돌아가던 상태라서 더 이상 최적화가 안되고 있는걸수도 있다. loss는 accuracy처럼 좋은 값이 정해져있는 지표가 아니라, 결과를 육안으로든 다른 지표로든 직접 사람이 확인해야 한다.