---
{"dg-publish":true,"permalink":"/ml/llm/persona-axis/"}
---

[https://arxiv.org/abs/2601.10387](https://arxiv.org/abs/2601.10387)

# llm의 hidden state

word embedding vector들의 sequence -attention→ hidden vector sequence

이때 hidden vector sequence를 행렬로 볼 수 있으니 이걸 hidden state.

# [[수학/선형대수/linear subspace\|linear subspace]]

# persona axis

hidden state를 이루는 벡터들은 모두 하나의 2,3차원짜리 linear subspace안에 존재하는데, 이 subspace가 대화에서의 persona를 정의한다.

특히 이 평면 안에서도 특정 방향으로 갈수록 해당 페르소나의 성향이 짙어지는데, 이걸 persona axis라고 부르기로 한거.

+) 시스템 프롬프트 필요없이, assistant 방향으로 더해주기만 해도 같은 효과가 나온다.

# persona drift

처음에 assistant로 설정해둬도, 대화 도중에 감정, 철학적 질문과 같은게 섞이면 subspace에서 이탈하여 다른 subspace로 이동하는 현상 발생한다.

이유는 attention 과정에서 새로 들어온 감정, 철학 벡터가 hidden state에 추가로 더해지며 기존의 persona가 약해지고 감정적 표현에 맞는 페르소나 쪽으로 이동하는 것.

→ persona drift!

# 분포

초기 층: 시퀀스에서 국소적인 의미, 문법 등을 처리하는 부분이라 persona 강하지 않다

중간 층: hidden state를 받아 본격적인 사고를 진행하는 층이라 persona 경향성이 가장 강하다

후기 층: 사고 바탕으로 구체적인 단어 선택에 집중해야 해서 persona 경향이 다시 약해짐