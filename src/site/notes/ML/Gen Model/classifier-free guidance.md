---
{"dg-publish":true,"permalink":"/ml/gen-model/classifier-free-guidance/"}
---

단어 임베딩을 쓰지 않는 경우, 넣어서 쓰는 경우 각각을 돌리고 나온 epsilon을 이용해 다음과 같이 조정. score의 방향을 조정해주는 거다.

$$ ε_{guided}=ε_{uncond}+s⋅(ε_{cond}−ε_{uncond}) $$
