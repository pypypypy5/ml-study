---
{"dg-publish":true,"permalink":"//onnx/"}
---

학습 완료된 모델을 inference 전용으로 뽑아내는 표준 규격.

.onnx로 만들어진다. pytorch는 .pth로.

내부적으로 가중치, 모델을 계산 그래프 형식으로 저장한다.

모델을 한번에 메모리에 올리고, onnx 런타임 엔진으로 굴려서 torch로 돌리는거보다 훨씬 빠르다.

```jsx
torch.onnx.export(
      model,                    # PyTorch 모델
      dummy_input,              # 예시 입력
      'best_model.onnx',        # 저장할 파일명
      export_params=True,       # 가중치도 저장
      opset_version=11,         # ONNX 버전
      input_names=['input'],    # 입력 이름
      output_names=['output'],  # 출력 이름
      dynamic_axes={            # 배치 크기 동적
          'input': {0: 'batch_size'},
          'output': {0: 'batch_size'}
      }
  )
```

로 onnx export.

```jsx
session = ort.InferenceSession(model_path)
outputs = session.run(
              [self.output_name],            # 출력 이름
              {self.input_name: input_tensor}  # {입력이름: 데이터}
          )
```

onnx 모델은 이렇게 불러오고, 실행한다.
# onnx runtime
런타임은 c++. 즉 밖의 언어가 무엇이든 입력만 받고 전부 내부적으로 c++로 돌리니 파이썬 호출과 같은 오버헤드가 여기서는 없다.

### [[개발/Intermediate Representation\|Intermediate Representation]]
