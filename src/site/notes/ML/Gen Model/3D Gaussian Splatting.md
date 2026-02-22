---
{"dg-publish":true,"permalink":"/ml/gen-model/3-d-gaussian-splatting/"}
---

# 문제
[[ML/Nerf\|Nerf]]는 픽셀 하나 체크, 학습하는 시간이 너무 많이 들었다. 또한 공간의 모든 픽셀을 체크해야 하니 더더욱 느리다.
-> 빈 공간은 무시하고, 메쉬를 시점에 투영해 빠르게 돌리자.
# 원리
1. 여러 방향에서 본 이미지를 바탕으로 feature point를 따는 rule base로 여러 [[확률-통계/Gaussian Distribution\|Gaussian Distribution]]인 구슬들을 무수히 공간에 init. 
2. 해당 시점에서 봤을때의 이미지를 만들고, 이게 실제 이미지에 맞는지 확인 후 오차를 다시 공간상의 구슬들에 반영한다. 이때 각 구슬의 타원 방향, 색, 투명도가 조정되며 보다 실제 3d 공간에 가까워진다.
3. 1,2를 반복하며 점점 공간이 실제와 비슷해진다.


여기서 파생되어 나온 것이 [[ML/4D Gaussian Splatting\|4D Gaussian Splatting]]이다.
# 참고 자료
https://gemini.google.com/share/56f96813db67