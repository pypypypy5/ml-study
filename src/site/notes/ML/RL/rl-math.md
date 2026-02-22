---
{"dg-publish":true,"permalink":"/ml/rl/rl-math/"}
---

# **policy 대한 reward의 수렴 증명**

$$ \theta^*= \arg\max_{\theta}\frac{1}{T}\sum_{t=1}^{T}\mathbb{E}_{(s_t,a_t)\sim p_\theta(s_t,a_t)}\left[r(s_t,a_t)\right] $$

$$ \mu = \begin{bmatrix} P(s_1, a_1) \\ P(s_1, a_2) \\ P(s_2, a_1) \\ P(s_2, a_2) \\ P(s_3, a_1) \\ P(s_3, a_2) \end{bmatrix} = p_\theta(s,a) $$

$$ \mu = \mathcal{T}\mu $$

여기서 다음 확률 분포로의 이동 T가 선형이 보장되는 이유는,

$$ p_{t+1}(s') = \int p(s'|s, a) p_t(s) ds (확률들의 가중합이 다음 확률) $$

결국 수렴 상태인 mu는 T의 [[수학/선형대수/Eigenvector\|eigenvector]]가 된다. ([[수학/선형대수/eigenvalue\|eigenvalue]]는 1)

# **정상 분포 찾기**

그래서 mu를 구하려면 T 행렬의 eigenvector 찾으면 되지만, T를 직접 구하는건 어렵다. 그래서 대신 쓰는 방법이,

## 샘플링으로 근사 ([[ML/RL/monte carlo\|monte carlo]])

적당히 오래 굴려보면 결과가 mu에 수렴할 것.

## [[ML/RL/bellman equation\|bellman equation]]

$$ V(s) = E[r + \gamma V(s')] $$

이 식을 반복적으로 풀다 보면 v가 특정 점으로 수렴하고, 이게 바로 고유 벡터 되는 것.