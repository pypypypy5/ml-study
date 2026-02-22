---
{"dg-publish":true,"permalink":"///svd/"}
---

[[수학/선형대수/Eigenvector\|Eigenvector]] → [[수학/선형대수/Eigenbasis\|Eigenbasis]] → [[수학/선형대수/Spectral Decomposition\|Spectral Decomposition]] → svd로 확장해나가는 과정이다.
[https://chatgpt.com/share/691860f2-e2cc-8008-8921-6035e7e6812b](https://chatgpt.com/share/691860f2-e2cc-8008-8921-6035e7e6812b)

$M=U\sigma V^*$

M (mxn): 원래 행렬

U (mxm): 좌특이 행렬. AAT의 eigenvector들, 즉 좌특이 벡터들을 열로 가지는 ortogonal matrix

Sigma (mxn): 특이값 행렬. 일부가 각 원소에 특이값을 가지는 대각 행렬이고, 그 외 빈 공간은 차원을 지우거나, 늘리기 위한 부분

V_T (nxn): 우특이 행렬. ATA의 eigenvector들, 즉 우특이 벡터들을 행으로 가지는 ortogonal matrix

U와 V_T에서 특이 벡터들은 각 특이값의 크기가 큰 순서대로 정렬. eps_1>eps_2… 하는 식으로.

특이값들은 각 eigenvector들의 제곱근.

1. 변환의 연속으로 보는 관점

근본적으로 spectral과 유사하다.

행렬을 간단하게 변환하기 위해

V_T에서 앞서 말한 “singular basis”로 변환 후

Sigma에서 stretch, 차원 지우거나 덧붙이고

U에서 원래 기저로 다시 되돌리기를 수행하는 것.

2. rank-1 행렬들의 합으로 보는 관점

$$ A=∑rσ_iu_iv_iT $$

rank-1이라는건 열벡터, 행벡터 모두 하나의 방향만 표현한다는 것. 즉 행렬이 하나의 방향만 담고 있음. 또한 i가 낮을수록 영향 큰 변수. 행렬을 각 주요 방향들로 분할하여 영향 큰 방향만 남겨도 어느정도 의미가 유지되는 것.
# 다른 해석
여기서 확장하여, 유사한 과정을 ATA, AAT에 실행한다.

1. ATA는 A가 입력 벡터에 가하는 변환의 크기를 측정하는 것.

n →(A)→ m → (AT) → n의 방식으로 차원을 n→m→n으로 옮긴다.

(Av)^2=vT(ATA)v이므로, ATA는 변환이 v에 얼마나 scale 하는지를 제곱으로 측정하는 것.

ATAv=lambda*v이므로 이걸 정리하면 (Av)^2=lambda, 즉 sqrt(lambda) = singular value.

즉, sigular value는 각 성분이 A를 통해 얼마나 scale 되는지를 다룬다.

그러므로 VT를 곱함으로써 입력 벡터를 ATA의 고유벡터인 v_j들로 분해하고, S를 곱해 singular value를 곱하여 scale.

1. 성분 별 분해

v_j의 정의와 관련된 식을 변형하면 이렇게 나오고, u_j는 AAT, 즉 출력공간의 크기 1인 고유벡터다.

$$ Av_j=s_ju_j $$

즉, A에 v_j를 넣으면 정확히 u_j 방향으로 s_j만큼 scale되어 출력된다.

종합하여, 벡터를 v_j 방향으로 분해 → s_j로 scale → u_j로 출력 공간에서 재구성.

이 과정을 모든 기저 방향, 즉 v_j로 반복, 다 더하면 변환 완료된 벡터가 나온다.

$$ A=∑s_ju_jv_j^T $$

**TODO**

정보 압축에 대해 보다 자세히. 수학적으로 더 엄밀히, 디테일하게 파서 정보 압축 자체에 대한 이해도 높여서, ml에 필요한 선대, 정보이론 파고들기.