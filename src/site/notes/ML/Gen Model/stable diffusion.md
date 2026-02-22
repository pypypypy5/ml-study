---
{"dg-publish":true,"permalink":"/ml/gen-model/stable-diffusion/"}
---

diffusion은 그럴듯한 이미지를 만들지만 내가 원하는 의도 반영해서 그릴 수 없다.

→ 단어 임베딩을 cross attention으로 반영하자!

→ 그러나 단어 임베딩을 바로 반영하면 모델이 단어 지시를 따라가는데에만 집착해서 자연스러운 manifold에서 멀어짐.

→ 자연스러움과 지시 사이를 조정해야.

보다 자세히는,

**[[ML/Gen Model/classifier-free guidance\|classifier-free guidance]] (CFG)**

단어 임베딩을 쓰지 않는 경우, 넣어서 쓰는 경우 각각을 돌리고 나온 epsilon을 이용해 다음과 같이 조정. score의 방향을 조정해주는 거다.

$$ ε_{guided}=ε_{uncond}+s⋅(ε_{cond}−ε_{uncond}) $$

[[ML/Gen Model/SDXL\|SDXL]]
