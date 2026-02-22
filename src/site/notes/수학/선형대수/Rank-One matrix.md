---
{"dg-publish":true,"permalink":"///rank-one-matrix/"}
---

# 정의
$\Delta = u v^T$ 식으로, 두 벡터를 곱해 만든 행렬
# 특성
어떤 벡터를 이걸로 변환하건, 이 변환의 결과 벡터의 방향은 언제나 같다. (특정 벡터에 스칼라 곱을 한 것과 동일)
## 이유
$\Lambda$가 $d_{out} \times 1$ 칼럼 벡터이고, $v$가 $d_{in} \times 1$ 칼럼 벡터라면, $u v^T$는 $d_{out} \times d_{in}$ 크기의 행렬.
$$\Delta x = (u v^T) x = u (v^T x)$$
-> x가 무엇이건, $v^T$와 곱해지며 스칼라가 된다.
-> 출력의 방향은 u의 방향으로 고정.