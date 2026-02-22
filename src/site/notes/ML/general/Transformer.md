---
{"dg-publish":true,"permalink":"/ml/general/transformer/"}
---

[[ML/general/self-attention\|self-attention]] 구조

범용적으로 사용될 수 있는 아키텍처. 입력을 토큰으로 쪼개고, 각각의 토큰을 벡터로 임베딩한다.

1. 이 토큰이 다른 토큰과 어떤 연관이 있는가, 를 묻기 위해 각 토큰에 query 행렬을 곱하고,
2. 각 토큰에 key 행렬을 곱해서 나온 벡터들을 나열,
3. key 벡터들을 query 벡터들과 내적해 나온 scalar들로 행렬을 만든다. 이때 결과로 나온 행렬의 각 요소는 해당 인덱스 토큰끼리의 연관도.
4. 행렬을 [[ML/general/softmax\|softmax]]로 정규화한다. (next token prediction인경우 학습시 다음 토큰 직접 보고 맞히도록 학습하는 것을 방지하기 위해 해당 인덱스 이후의 토큰과 연산한 결과는 -inf 처리, softmax 결과가 0이 되도록 한다.)
5. value matrix와 토큰들 다시 곱하고, 아까 key 행렬 곱했던 순서대로 다시 각 열에 곱한다. 그럼으로써 아까 얻은 토큰끼리 연관도를 value 벡터에 직접 scalar 곱하여 반영한다.
6. value 벡터들 열끼리 모두 더해 최종 임베딩 변경 만들고, 해당 변경된 벡터를 원래 토큰에 더하여 반영, attention 종료

[[ML/multi head attention\|multi head attention]]은 이 attention을 병렬로, 서로 다른 q,k,v 행렬로 진행, attention 종료 후 나온 변경값을 모두 더해 토큰 wise로 더한다.

각 헤드는 서로 다른 feature를 다루도록 학습한다. 하나는 문법을 다루고, 하나는 형용사와 명사 사이 관계 다루고 하는 식으로.

**[[ML/theory/Invariance\|Invariance]] (불변성)**

F(Tx)=F(x)

어떤 변환 T를 입력에 해도 결과는 같다는 것.

cnn은 이미지 옆으로 살짝 옮겨도 똑같이 객체 잡아내니 invariance.

**[[ML/theory/Equivariance\|Equivariance]] (공변성)**

F(Tx)=T(Fx)

두 변환을 어느것을 먼저 하건 결과가 같게 나온다는 것.

일반 attention은 토큰 순서 뒤섞어도 결과가 똑같이 나온다. 순서 관계없이 토큰들 사이의 관계만을 생각하기 때문에 그런 것이며, 때문에 positional encoding이 필요한 것이다.

**[[ML/Positional encoding\|Positional encoding]]**
self-attention은 permutation에 대해 [[ML/theory/Equivariance\|Equivariance]]하여 순서가 상관이 없으니 모델이 순서를 이해하며 학습할 수 있도록 토큰 벡터에 [[ML/Positional encoding\|Positional encoding]] 벡터를 더해 순서 정보를 주입한다.

이때 이렇게 더해도 정보가 손상되지 않는 이유는 sin, cos 방식으로 일정한 형식으로 정보를 넣는것이므로 모델이 학습하여 순서 정보를 분리, 원본 정보를 손상 적게 이해하는 것이 가능하기 때문이라 한다.

인코딩 방식은 여러개 있지만 대표적으로 다음 수식을 쓴다.

$$ p_{j,2i}=sin(100002i/dj), p_{j,2i+1}=cos(100002i/dj) $$

너무 무거워서 보통 [[ML/general/batch normalization\|batch normalization]] 대신 **[[ML/general/Layer Normalization\|Layer Normalization]]** 많이 쓴다.

# vision

범용 아키텍터라 비전 문제 푸는데 **[[ML/vision/ViT\|ViT]]**, **[[ML/vision/swin transformer\|swin transformer]]** 쓸 수도 있다. 
