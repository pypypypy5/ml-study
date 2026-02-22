---
{"dg-publish":true,"permalink":"/ml/llm/nested-learning/"}
---

https://arxiv.org/abs/2512.24695

# 방법론
신경망과 optimizer를 이전의 정보와 현재 피드백의 차이 - surprise에 따라 몰랐던 정보를 업데이트하는 시스템이라고 바라본다. momentum과 같은 학습 기법은 단순히 학습 기법이 아니라 이전의 정보들을 압축해서 기억해두는 일종의 방식이라고 바라보는 것.

## HOPE
= self-referential titans + mlp
### titans
단기 기억 담당. 
1. 메모리 - q, k, v matrix가 고정된 일반 transformer와 달리 입력을 받고 내용을 기억하기 위해 지속적으로 변하는 가중치를 가진다. 인간의 작업기억과 같이 입력을 받아 중요 내용을 업데이트하고, 사전 기억을 바탕으로 처리된 정보를 뒤의 mlp에 보낸다.
2. 목적 - 입력을 받은 후 먼저 이중에 무엇이 중요한지, 무엇을 기억해야 할지를 goal로 만든다. 이후 업데이트가 진행될때 이 목적을 바탕으로 단기기억의 prior를 업데이트 하는 것.
3. 업데이트 - [[ML/L2-Regression\|L2-Regression]]을 이용한 [[ML/Gradient Descent\|Gradient Descent]]
   $$M_t = \underbrace{M_{t-1}(\alpha_t I - \eta_t k_t k_t^T)}_{\text{① 낡은 기억 지우기}} + \underbrace{\eta_t \hat{v}_t k_t^T}_{\text{② 새로운 기억 심기}}$$
   - **$\alpha_t$ (Forget Gate):** 과거의 기억($M_{t-1}$)을 얼마나 유지할지 정합니다. (1이면 다 기억, 0이면 다 망각) 
   -  **$-\eta k k^T$ (Correction):** 현재 입력($k$)에 대해 이미 알고 있는 잘못된 정보 방향을 깎아냅니다.
   - **$+\eta \hat{v} k^T$ (Learning):** 현재 입력($k$)과 스스로 만든 목표($\hat{v}$) 사이의 새로운 연결을 메모리에 더합니다.
구현상으로는 일반 softmax [[ML/general/Transformer\|Transformer]]보다 [[ML/RNN\|RNN]], [[ML/Linear Attention\|Linear Attention]]에 가깝다. 
### mlp
장기 기억, 사고 담당.
앞의 titan에게서 정보를 받고 장기기억을 바탕으로 작업을 최종 처리한다. 