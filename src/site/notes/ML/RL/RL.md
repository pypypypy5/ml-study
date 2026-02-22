---
{"dg-publish":true,"permalink":"/ml/rl/rl/"}
---

[[ML/RL/off-policy\|off-policy]] <-> [[ML/RL/on-policy\|on-policy]]
<-> [[ML/RL/offline\|offline]]
# 정의
현재 state에서 적절한 action을 학습시키는 것. 이때 기본적으로 상황을 markov process로 가정하여, 바로 지금 state의 정보만으로 다음 state를 완벽하게 예측할 수 있다고 본다.

state-action 쌍들의 연속, 즉 특정 trajectory가 나올 확률은 다음과 같다.

$$ p_\theta(s_1, a_1, \ldots, s_T, a_T)= p(s_1)\prod_{t=1}^{T} \pi_\theta(a_t \mid s_t)\, p(s_{t+1} \mid s_t, a_t) $$

theta는 파라미터.

최종 목표는 ml에서 맨날 보는 [[확률-통계/MLE\|MLE]]. trajectory의 총 보상을 극대화하는 theta를 찾는 것이다.

$$ \theta^*= \arg\max_{\theta}\mathbb{E}_{\tau \sim p_\theta(\tau)}\left[\sum_t r(s_t, a_t)\right] $$

그걸 하려면 일반 ml에서 loss를 구하듯이 현재 policy의 성능을 평가해야 하는데, 그러려면 결국 argmax 뒤의 [[ML/RL/reward\|reward]] 합을 구하면 그게 바로 성능이 되는 것. 그런데 T가 많거나, 무한할 경우 현재 성능을 평가할 수 없다. 대신 t가 충분히 커지면 r은 수렴하고, 그에 따라 전체 r의 평균인 성능도 수렴하므로 그냥 수렴점만 구하면 다 돌리지 않고 성능을 알 수 있다. 수렴의 증명은 아래 참조.

# 수학적 정당화
[[ML/RL/rl-math\|rl-math]]

# **[[ML/RL/value function\|value function]]**
현재 하나의 s,a 대한 reward 아니라 특정 상태, 혹은 action에 대한 장기적인 가치를 나타내는 것.

1. state-value function
2. action-value function: [[ML/RL/Q-function\|Q-function]]



### **[[ML/RL/Policy Improvement Theorem\|Policy Improvement Theorem]]**
policy를 이렇게 업데이트하면 발전이 보장됨을 증명하는 것. rl 전반에서 중요하게 쓰인다.


# 방법론
## **[[ML/RL/policy gradient\|policy gradient]]**

## [[ML/RL/model-based rl\|model-based rl]]

## [[ML/RL/actor-critic\|actor-critic]]

## [[ML/RL/Q-learning\|Q-learning]]


# [[ML/RL/Exploration\|Exploration]]
에이전트가 현재 방식만을 고수하고 다른 시도를 안한다.
-> 안해본 전략을 탐색하도록 하는 것. 이게 exploration
반대로 현재 전략을 사용해 안정적으로 결과 뽑아내도록 하는 것은 [[Exploitaion\|Exploitaion]]


# 문제

# **behavioral cloning의 문제**

전문가는 익스트림한 실수를 하지 않는다. 그런데 그걸 학습한 모델은 조금씩 실수하며 오차가 누적되고, 결국 학습 데이터에 없는 상황이 나왔을때 어떻게 처리할지를 모른다.

그걸 해결하기 위해

1. [[ML/general/Data Augmentation\|Data Augmentation]] - 정방향으로 가는 차의 옆에 카메라 달아 사진찍고, 이 경우에는 옆으로 핸들 꺾어서 되돌린다, 를 학습시킴
2. [[ML/RL/DAgger\|DAgger]] - 전문가가 모델이 운전하는걸 보고 있다가 실수하면 그때 그때 어떻게 해야 하는지 정정하며 라벨 달아주기.
3. 더 큰 모델

## **multimodal behavior 문제**

바로 앞에 나무 있을때 왼쪽으로 꺾어도 오른쪽으로 꺾어도 되는 상황에서 오히려 두 선택지가 비등하면 두 선택지를 평균내서 나무에 박아버린다.

해결은,

1. 복잡한 확률 분포 - MoG, [[ML/Gen Model/Diffusion\|Diffusion]], Latent variable diffusion이 요즘 로보틱스에서 유명한데, 지금 바로 다음 action 하나만 뽑는 것이 아니라 diffusion 이용해서 다음 action들의 sequence 자체를 한번에 뽑아보리는 것. jitter 없고, sequence가 더 자연스러워진다.
2. discretization - 연속적인 선택지 대신 좌로 30도, 우로 30도로 끊어버리기.
3. 이전의 정보 추가 - Transformer, lstm과 같은 방식으로 직전 상태 뿐 아니라 이전의 프레임들도 모델에 넣어주기.

지나치게 모델이 변동하고, 중요한 능력을 잃어버릴 수 있고, 그걸 막기 위해 [[정보 이론/KL-Divergence\|KL-Divergence]]를 반영한 목적 함수를 만들어 이전 분포에서 달라지는데에 패널티를 주어 과도한 변동을 막는다. [[ML/RL/PPO-KLD\|PPO-KLD]]라고 하더라.

# 용어
### [[ML/RL/episode\|episode]]