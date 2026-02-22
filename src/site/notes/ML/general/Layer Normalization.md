---
{"dg-publish":true,"permalink":"/ml/general/layer-normalization/"}
---

cnn은 batch normalization을 쓰지만 transformer는 너무 커서 batch 처리를 하기 어렵고, 시계열 분석, nlp의 경우 매번 시퀀스마다 통계 특성이 크게 달라 정규화 어렵다. 오히려 정규화를 함으로써 데이터에 왜곡이 생기는 것.

그래서 배치 대신 토큰 하나마다 내부 벡터의 요소 값들을 대신 정규화한다.