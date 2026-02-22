---
{"dg-publish":true,"permalink":"/ml/theory/manifold-hypothesis/"}
---



[[수학/해석학/manifold\|manifold]]

manifold hypothesis는 데이터가 고차원 공간의 이 manifold에 몰려있을 것이라는 경험적 가정이다.

ex) [[ML/Gen Model/Auto Encoder\|Auto Encoder]]에서 고차원 데이터를 저차원 데이터로 압축, 중요한 feature만 뽑아내는데, 이때 데이터의 각 점은 manifold 위에 모여있고, 따라서 저차원으로 “좌표 전사”하여 표현이 가능한 것.

데이터가 모두 하나의 거대하고 복잡한 manifold 위에 있을 수도 있고, 자연 사진은 a manifold에, 사람 사진은 b manifold 위에 있는 식으로 여러개의 각각에 있을수도 있다.

가장 일반적인 가정은, 하나의 복잡하고 거대한 manifold가 있고, 그 안에 자연, 사람과 같은 submanifold가 있을것이라는 것.

encoder는 고차원 데이터를 선형변환 (pca와 같이) 하여 manifold 위의 좁은 “패치”로 변환하는 과정인 것이다. (사실 러프한 이야기고, 실제로는 manifold가 복잡하게 꼬여있으면 비선형성이 필요하다.)

+) [[ML/train/natural gradient\|natural gradient]]는 fischer 정보로 정의된 통계적 manifold 위에서 gradient descent 하는 것.