---
{"dg-publish":true,"permalink":"//kl-divergence/"}
---

두 분포 사이의 거리, 즉 두 분포 사이의 차이를 나타낸다. rl의 ppo에서 썼었다.

$$ D_{KL}(P\|Q) = H(P, Q) - H(P) $$
다른 의미로는 P를 Q로 모델링했을때의 [[정보 이론/Entropy\|Entropy]]에서 P의 [[정보 이론/Entropy\|Entropy]](최적값)와 차이가 되는 것.

= 현재 모델로 실제 설명할때 나오는 엔트로피와 최적 모델 엔트로피 사이 차이