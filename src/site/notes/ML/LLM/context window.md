---
{"dg-publish":true,"permalink":"/ml/llm/context-window/"}
---

[[ML/general/Transformer\|Transformer]]에서 단순히 kv cache가 너무 무거워서. 토큰 하나당 3메가 정도 용량이 생기는건데, 앞의 텍스트가 길어질수록 비례해서 kv cache가 무거워지고, 그래서 context window를 제한하는것.