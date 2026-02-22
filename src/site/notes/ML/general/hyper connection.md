---
{"dg-publish":true,"permalink":"/ml/general/hyper-connection/"}
---


$H_t = \sum_{i=1}^{t-1} h_i$

모든 층을 서로 skip connection. 이전의 모든 신호를 받게 하여 신호 감쇠 문제를 줄인다

## 문제

1. 너무 많이 들어와서 신호가 터진다.
2. 이전 모든 레이어의 모든 신호를 저장해두고, 가져다 쓰니 시스템 부하가 생긴다