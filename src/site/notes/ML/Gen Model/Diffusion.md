---
{"dg-publish":true,"permalink":"/ml/gen-model/diffusion/"}
---

원본 이미지에 가우시안으로 노이즈를 계속 추가한다. 노이즈를 여러 스텝에 걸쳐 추가해 기존 정보가 모두 사라진 순수 노이즈로 만들고, 다시 reverse 과정을 거치며 노이즈를 차차 지워가면서 원래 이미지로 복원하는 것.

**가우시안 노이즈를 쓰는 이유**

1. 여러 스텝을 거치며 계속 겹쳐져도 같은 가우시안 노이즈, 분포가 복잡해지지 않는다.
2. 분산을 이용해 얼마나 원본에서 파괴된건지를 측정할 수 있다.
3. 정보 이론적으로 가장 무작위라 빠르게 무작위 노이즈 상태에 도달할 수 있다.

**과정**

t 시점의 이미지는 이전 x_t-1에 의해 다음과 같이 변형된다.

$$ x_t=\sqrt{α_t}x_{t−1}+\sqrt{1−α_t}z_t,z_t∼N(0,I) $$

보다 크게 보면,

$$ x_t=\sqrt{αˉ_t}x_0+\sqrt{1−αˉ_t}ε $$

alpha는 학습되는 값이 아닌 미리 결정해둔 상수로, 루트를 씌우는 이유는

$$ Var(x_t)=α_tVar(x_{t−1})+(1−α_t)Var(z_t) $$

와 같이 분산으로 만들었을때 깔끔하게 나오도록 하기 위해서.

이렇게 깔끔하게 나오면 위의 x_t, x_0 식이 나올 수 있고, 그렇게 해야 나중에 reverse에서 학습이 안정적으로 될 수 있는 closed form이 된다.

reverse 과정에서는 역으로 거슬러올라가며 x_t로부터 x_t-1 사이의 노이즈가 뭐였는지 예측해간다. 노이즈 예측해서 스케일링 후 빼고, 다시 랜덤 변동을 추가한다.

그렇게 하는 이유는 diffusion이 확률 분포를 샘플링하도록 훈련시키기 위함. 말이 되는 manifold 상의 데이터들 분포를 학습시키는 것이 목표인데, 단순히 노이즈를 바로바로 지워내면 분포가 아니라 하나의 점으로만 수렴한다.

$$ x_{t−1}=μ_θ(x_t,t)+σ_tz $$

이렇게 x_t-1을 예측하고, mu는 alpha, beta의 정보도 함께 고려해서 계산한다.

loss는 다음과 같다. 결국 각 노이즈의 mse가 loss가 되는 것.

$$ L=E_{x_0,t,ε}[∥ε−ε_θ(x_t,t)∥^2] $$

reverse에 실제로 쓰는 아키텍처는 [[ML/segmentation/u-net\|u-net]]. [[ML/segmentation/segmentation\|segmentation]]에 쓰는 바로 그 아키텍처로, 같은 u net을 [[ML/RNN\|RNN]] 식으로 반복 호출하여 픽셀마다 노이즈를 예측하게 한다. 물론 지금의 t가 얼마인지 인식시키기 위해 [[ML/Positional encoding\|Positional encoding]]도 넣는다.

**ml적 의미 - 직관**

diffusion은 epsilon을 예측해 지워나간다는 표면적 의미를 가지지만, 직관적으로는 노이즈를 말이 되는 데이터가 모인 manifold로 점진적으로 움직여간다는 의미를 가진다. 더 그럴듯한 데이터 쪽으로 움직이는걸 반복하는 것.

score라고 표현하며, 더 확률 밀도가 높은 (=더 말이 되는 데이터가 몰려있는) 쪽으로 움직여가는 것.

$$ score(x_t)=∇x_tlogp_t(x_t) $$

그런데 score를 바로 구하는것은 어렵다. 그래서 가우시안 노이즈일때 score와 비례 관계인 epsilon을 구하는 것.

**[[수학/ODE\|ODE]] (보통 미분방정식)**

$$ dx/dt=f(x) $$

**[[수학/SDE\|SDE]] (확률 미분방정식)**

ode에 랜덤 변수를 섞은 것.

$$ dx=f(x)d_t+g(t)dW_t $$

diffusion의 reverse와 정확히 같다.

$$ dx=(forward drift−노이즈 세기^2×score)dt+노이즈dWˉt $$

이런 방식을 [[DDPM\|DDPM]]이라 한다.

그런데 이 방식은 step 1000씩 하고 너무 많고 무거움. 그리고 u net을 썼을때 경로는 상당히 일관적으로 나온다. 그렇다면 random noise를 없애고 쭉쭉 바로 score 따라서 20 step 정도만에 도달해도 되지 않나.

그렇게 하는게 [[DDIM\|DDIM]]이고, 이건 ODE에 가깝다. 다만 결정론적으로 하나의 점에 도달하게 되고, 이걸 조절하기 위해 랜덤성 계수를 두어 조절한다.

diffusion은 그럴듯한 이미지를 만들지만 내가 원하는 의도 반영해서 그릴 수 없다.
-> **[[ML/Gen Model/stable diffusion\|stable diffusion]]**


### diffusion이 좋은 이유
1. [[ML/Gen Model/VAE\|VAE]]는 [[정보 이론/KL-Divergence\|KL-Divergence]] 때문에 강제로 정규분포로 만들어지며 무엇보다 latent가 저차원이니 디테일한 정보들은 손실이 생기고, 정규분포로 변형된 저차원 구조의 E[x|z]이니 결과는 무난하고 평균적인, 흐릿한 값이 된다는 것.
2. diffusion은 직접 [[확률-통계/log likelihood\|log likelihood]]를 최적화해서 디테일하고 샤프한 결과를 낼 수 있다.
3. 안정적으로, 단계별로 진행되는거라 중간중간에 필요한 것들을 끼워넣어서 조작할 수 있다. ex. mask, [[ML/Gen Model/ControlNet\|ControlNet]] 등등