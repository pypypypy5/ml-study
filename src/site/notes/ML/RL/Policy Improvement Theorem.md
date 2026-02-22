---
{"dg-publish":true,"permalink":"/ml/rl/policy-improvement-theorem/"}
---


$$ \pi'(\mathbf{a}|\mathbf{s}) = 1 \text{ if } \mathbf{a} = \arg\max_{\mathbf{a}} Q^{\pi}(\mathbf{s}, \mathbf{a}) $$

새 정책을 만들때 Q가 가장 높은 a에 몰빵하기 (확률 1을 부여)

→ 새 정책이 이전 정책보다 낫거나 최소한 같다.