---
{"dg-publish":true,"permalink":"/ml/segmentation/dice/"}
---

[[ML/segmentation/segmentation\|segmentation]] 문제 푸는 모델에서 [[ML/general/loss\|loss]]로 [[정보 이론/Cross Entropy\|Cross Entropy]] 대신 많이 사용. 각 픽셀의 확률을 직접 반영하는게 아니라,

- GT 영역 집합: Y
- 예측된 영역 집합: X

$$ Dice(X,Y)=2∣X∩Y∣/∣X∣+∣Y∣ $$

식으로 예측 성공한 픽셀들의 비율을 재는 것.

ce 안쓰고 이렇게 하는 이유는, ce를 쓰면

특히 클래스 불균형이 심한 경우(작은 종양, 작은 object 등)에서:

- CE는 배경 픽셀이 너무 많으면
    
    → 배경만 잘 맞춰도 loss가 꽤 작아짐.
    
- Dice는 “전체 영역 overlap 비율”이라
    
    → 작은 object도 겹치는지 안 겹치는지에 민감.