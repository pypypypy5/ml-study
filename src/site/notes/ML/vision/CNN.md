---
{"dg-publish":true,"permalink":"/ml/vision/cnn/"}
---

**convolution layer**

32_32 이미지가 rgb로 3장, 32_32*3의 형상을 가지고, 하나의 필터는 이 r,g,b 각각에 대해 모두 convolution 수행하여 텐서 만들고 그 세장을 모두 element wise로 더하고 편향까지 더하면 하나의 feature map이 나옴.

필터가 32장이면 모두 병렬로 수행하여 32장의 feature map이 나오고, 결국 출력 형상은 32_32_32.

pooling

pooling은 2*2면 해당 부분 4개 중 가장 값이 큰 요소를 가져와서 그것만 남기는 것. 이로써 중요한 feature만 남기는 작업 한다.

ex. 2_2 필터에 2 stride면 32_32 → pool → 16*16

**실무 팁**

1. conv → [[ML/general/batch normalization\|batch normalization]] → [[ML/general/relu\|relu]]가 한 묶음으로 이루어지는게 일반적. cnn은 파라미터가 많고 복잡해서 매 conv 계층 뒤마다 매번 bn을 하는게 일반적이라고 한다, 특별한 이유 없으면 무조건 넣는다고.
2. relu를 쓰는 이유는 그냥 무난해서. 별다른 이유 없으면 relu 쓴다 함.
3. 특별한 이유 없으면 padding을 적절히 넣어서 conv 층 지난 후에도 feature map 크기 유지되도록 하는 것이 좋다. conv 계층의 목적은 feature 추출이니 귀퉁이 부분 손실 없이 유지하는 편이 좋다는 것. ex. 3_3 filter, 1 stride면 padding 1 넣어서 32_32→32*32로 유지.
4. 파라미터가 커지면 과적합에 취약.
5. dropout: 과적합을 피하기 위해 학습 과정에서만 확률적으로 일부 노드를 비활성화시켜 장애를 주고 학습시키는 것. evaluate나 프로덕션에서는 출력 총값을 보정하기 위해 확률만큰 출력 크기를 스케일링한다. cnn에서는 마지막의 feature map을 확률 분포로 변환하는 fc layer에서 파라미터 너무 커지므로 과적합 취약하기에 사용한다.
6. [[ML/general/skip connection\|skip connection]]: 기울기 소실을 막기 위해 고정 파라미터 1로 앞의 기울기를 뒤에 바로 전달.
7. [[residual block: skip connection을 구현하기 위해 resnet에서 쓰인다. conv~ 블록을 하나의 residual block으로 감싸고 block의 input을 block의 output에 더한걸 쌓아 전체 신경망 구현.
8. 데이터 전처리 - 학습용 이미지를 자르고, 반전시키는 등 왜곡을 주어 모델이 더 강건하게 학습할 수 있도록 하고 과적합 막는다. (eval용 데이터는 원본 그대로) + 학습용 데이터를 normalize하여 가중치 업데이트 일관성 줄 수 있도록 한다.