---
{"dg-publish":true,"permalink":"/ml/vision/swin-transformer/"}
---

일반 ViT는 cnn과 달리 토큰 단위로 잘라 토큰 외부의 픽셀들과 관계 보는게 어려움.

→ window 내부의 토큰끼리만 self-attention 하되, window를 레이어마다 조금씩 shift하여 옆 픽셀들과 관계를 이해할, 볼 수 있도록 한다.

+) hierarchical하게 토큰 수를 줄여나가되, 각 토큰의 차원수는 늘이며 각 토큰이 레이어를 지날때마다 더 깊은 정보를 가지도록 한다.

사실 잘 모르겠다. 나중에 더 보자.