---
{"dg-publish":true,"permalink":"//mutual-information/"}
---

한 변수의 값을 알때 다른 변수의 불확실성에 어떤 영향을 미치는지를 나타낸다.

$$ I(X;Y) = D_{KL}(p(x,y) \| p(x)p(y)) = H(X) - H(X|Y) = H(Y) - H(Y|X)

$$

실제 분포와 “둘이 독립이다”라는 가정의 모델의 [[정보 이론/KL-Divergence\|KL-Divergence]]가 되는 것. 
[[정보 이론/Entropy\|Entropy]]
