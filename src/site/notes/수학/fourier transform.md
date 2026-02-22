---
{"dg-publish":true,"permalink":"//fourier-transform/"}
---

### 푸리에 변환

여러 파동이 겹쳐있는데에서 각 구성 성분들을 분리하는 방법

[https://www.youtube.com/watch?v=spUNpyF58BY](https://www.youtube.com/watch?v=spUNpyF58BY)

**아주 러프한 진행 방식**

1. 파동들을 원점을 중심으로, 각 좌표계 스타일로 감는다
2. 그래프의 “무게중심”이 있다고 가정하자. 한바퀴에 파동의 얼마나 담을지를 변화시키면서 (한바퀴에 n초를 감기 = frequency) 그래프의 무게중심은 그에 따라 어떻게 위치가 변하는지를 관찰
3. 무게중심은 계속 원점에 가까이서 진동하다가 어느순간 갑자기 확 튄다 → 갑자기 튄 이 위치의 frequency가 이 파동의 진짜 진동수
4. 단순히 하나의 파장만 아니라, 여러 파동이 합쳐진 파동도 이렇게 변환하면 “무게중심”이 몇번씩 튀는데, 이 지점들이 구성 파동들의 주파수들.

정확히는, 복소평면상에서 오일러 공식을 사용해서 원형으로 회전하는것을 그리고, 그래프를 적분해서 “무게중심”을 만든다. 이 무게중심의 실수부가 위의 x좌표가 되는 것.

**[[수학/inverse fourier transform\|inverse fourier transform]]**
[[기초 cs/FFT\|FFT]]
