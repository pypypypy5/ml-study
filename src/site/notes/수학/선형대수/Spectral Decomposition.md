---
{"dg-publish":true,"permalink":"///spectral-decomposition/"}
---


대칭 행렬을 간단하게 변환하기 위해 앞서 말한 eigenbasis를 이용해 변환 후 stretch하고, 다시 되돌리기를 수행하는 것. 대칭 행렬의 eigenvalue 다른 [[수학/선형대수/Eigenvector\|eigenvector]]들은 언제나 서로 수직이라는 점을 이용한다.

A=QDQ_T 로 정리된다. Q의 각 열은 [[수학/선형대수/Eigenvector\|eigenvector]]들이다. D는 대각 행렬로, 그러니 Q로 eigenbasis로 변환하고, D로 eigenbasis의 각 방향에 몇배를 곱하는지 정의하고, Q_T로 되돌린다. (orthogonal matrix의 transpose는 역행렬과 같으므로) +) orthogonal matrix는 회전을 수행

→ stretch 변환이 이루어지는 방향들(eigenvector)을 파악, 복잡한 행렬 아니라 “이쪽으로 변환 이뤄진다”고 단순화

혹은,
직교기저일 경우 벡터를 기저로 분해하여 나타내려면 VT, 변환한 좌표를 다시 벡터로 V.

v_jv_j^T는 곱해지는 벡터를 v_j에 투사하는 변환.

그렇게 한다면,

$$ S=∑λ_jv_jv_j^T $$

각 고유벡터로 벡터를 투사 후, 고유값 곱해 scale하는 과정을 모든 고유기저의 성분에 행하고 총합해 변환의 최종 결과 구하는 것.