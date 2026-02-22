---
{"dg-publish":true,"permalink":"/ml/gen-model/control-net/"}
---

[[ML/Gen Model/Diffusion\|Diffusion]]에서 결과물을 조작하는 방식으로 [[ML/Gen Model/stable diffusion\|stable diffusion]]에서 텍스트만 이용하는 대신, 더 디테일하게 포즈, 구도 등을 직접 조정하기 위해 직접 때려넣는다.
# 동작
## highlevel
1. diffusion의 u-net decoder를 떼어와서 따로 학습시킨다. 이게 controlnet.
2. 기존 u-net은 그대로 진행시키고, 병렬로 controlnet에 깊이, 포즈를 나타내는 이미지 데이터를 넣고 feature map으로 압축.
3. 압축된 feature을 일반 u-net의 feature map에 더한다.
4. 일반 u-net의 decoder가 controlnet 결과까지 더해진 feature map을 이미지로 복원.