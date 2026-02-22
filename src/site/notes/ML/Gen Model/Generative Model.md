---
{"dg-publish":true,"permalink":"/ml/gen-model/generative-model/"}
---

P_model이 P_data (실제 데이터 분포)를 근사하도록 훈련.

이후 P_model에서 랜덤 샘플을 추출하면 그것이 생성된 output이 되는 것.

이때 P_data는 데이터 내부의 핵심 feature를 뜻한다. 사물이 어디에 있고, 배색은 어떻게 되고, 와 같은 데이터의 정보들의 확률 분포를 P_model에 근사시키고, 모델에서 하나를 추출하면 그게 적절한 핵심 feature들을 담고 있는 생성물.

결국 데이터 분포를 근사시키는 문제기 때문에 두 분포 사이의 관계를 다루는 KL divergence 많이 나온다.
# 방법론

[[ML/Gen Model/Density estimation\|Density estimation]]
[[ML/Gen Model/Auto Regressive Model\|Auto Regressive Model]]
[[ML/Gen Model/Latent Variable Model\|Latent Variable Model]] (LVM)
[[ML/Gen Model/Auto Encoder\|Auto Encoder]]
Variational Auto Encoder ([[ML/Gen Model/VAE\|VAE]])