---
{"dg-publish":true,"permalink":"/ml/theory/local-minimum/"}
---

결론만 말하면 [[ML/general/loss\|loss]] landscape 위에 전역 최솟값이 하나만 있는게 아니라 엄청나게 많이 존재하며, 차원이 높아지면 (뉴런이 많아지면) 이 최솟값들이 [[수학/해석학/manifold\|manifold]]를 이루며 안장점을 형성하기 때문. 따라서 최솟값이 사방이 갇힌 곳에 존재하는 것이 아니라 "계곡"을 이루며 학습이 진행되며 결국 여기로 흘러내리기가 쉽다. 

최솟값이 많은 이유는 근본적으로 [[ML/theory/Permutation Symmetry\|Permutation Symmetry]], [[ML/Continuous Symmetry\|Continuous Symmetry]] 때문. 뉴런들이 서로 [[ML/theory/Equivariance\|Equivariance]]하기 (개성이 없기) 때문에 가능한 최솟값이 n! (n개 뉴런의 순서 변경)만큼 존재하는것이다.

# 참고
https://www.youtube.com/watch?v=2qXF8JHcU5E&t=18s
https://gemini.google.com/share/5cbd963d75ed