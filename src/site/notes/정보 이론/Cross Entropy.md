---
{"dg-publish":true,"permalink":"//cross-entropy/"}
---

cross entropy: P를 Q로 근사하여 인코딩했을때 얼마만큼의 추가 [[정보 이론/정보량\|정보량]]이 필요한지를 나타내는 것이다.

$$ H_p(q) = H(P, Q) = - \sum_{x \in X} p(x) \log q(x) $$
쉽게 말해서,
- 실제 분포는 p인데, 잘못 알고 q를 기준으로 부호화할 때 드는 평균 코드 길이

$$H(p,q)=H(p)+D_{KL}(p∥q)$$

이고, D_KL는 “내 모델 q 때문에 추가로 낭비하는 비트 수"

