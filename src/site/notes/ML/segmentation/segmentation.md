---
{"dg-publish":true,"permalink":"/ml/segmentation/segmentation/"}
---

매 픽셀 마다 클래스를 붙이는 문제. [[ML/segmentation/u-net\|u-net]] 많이 쓴다. 
[[ML/Gen Model/Diffusion\|Diffusion]]도 이거 쓴다.

큰 그림은 vae와 비슷하다. 정보를 cnn으로 압축한 뒤, 다시 convTranspose로 키워가면서 각 채널이 해당 위치 픽셀의 각 클래스에 대한 확률인 map으로 만드는 것. 다만 encoder에서 featrue map을 skip connection처럼 바로 연결, 채널에 그대로 추가함으로써 앞의 각 픽셀 정보를 추가한다.

[[ML/segmentation/DICE\|DICE]] loss

**실무**

pytorch 모델을 가져와서 학습시키는게 아니라. 아예 nnU net과 같이 내부 추상화된 모델을 들고와서 겉에서 데이터만 넣어주며 파인 튜닝할 수 있도록 하는 경우가 많다. 이게 훨씬 간단하다고 한다.

그래서 모델 훈련에 시간 쓰기보다, 데이터 전처리, 도메인 문제 정의하여 모델 trade off 생각하기 등이 주요하다고.

**3d cnn**

의료 도메인에서는 일반 이미지가 아니라 3차원 행렬을 각 채널의 내용으로 쓰는 경우 많다. 이 경우 cnn의 filter도 3차원, 똑같이 조금씩 움직이며 convolution 수행한다는건 똑같다.