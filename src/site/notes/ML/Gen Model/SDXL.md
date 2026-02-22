---
{"dg-publish":true,"permalink":"/ml/gen-model/sdxl/"}
---

일반적인 [[ML/Gen Model/stable diffusion\|stable diffusion]]는 텍스트를 하나의 encoder 통과시켜서 벡터 그룹 만든다. 다만 이렇게 하면 지나면서 지나치게 일반적인 feature 만 남는다는 것이 문제. 그런데 끝에서 2번째인 11 레이어의 feature는 보다 뾰족하게 feature 가 남고, 이걸 써먹는게 clip skip.

이런 일반화 문제를 구조적으로 해결하는 것이 sdxl로, clip L (12 레이어), clip G (24 레이어) 두개를 거친 두개의 벡터 그룹을 concat하여, G에서 일반적인, 넓은 범위의 feature, L에서 좁은, 날카로운 feature를 내도록 하여 문제를 해결한다.