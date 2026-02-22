---
{"dg-publish":true,"permalink":"/ml/general/reparametrization-trick/"}
---

VAE는 z를 바로 만드는 대신,

encoder가 평균과 표준편차를 출력하도록 한다.

$$ z=μ(x)+σ(x)⊙ϵ,ϵ∼N(0,1) $$

z를 나온 평균, 표준편차를 이용해서 만든다.