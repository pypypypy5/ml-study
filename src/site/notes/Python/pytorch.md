---
{"dg-publish":true,"permalink":"/python/pytorch/"}
---


**data**

변형:

```
transforms.Compose([
        transforms.RandomHorizontalFlip(),
        transforms.RandomCrop(32, padding=4),
        transforms.ToTensor(),
        transforms.Normalize((0.4914, 0.4822, 0.4465), (0.2023, 0.1994, 0.2010))
    ])
```

와 같이 transform 객체를 만들고,

```python
train_ds = datasets.CIFAR10(root=data_dir, train=True, download=True, transform=train_transform)
test_ds = datasets.CIFAR10(root=data_dir, train=False, download=True, transform=test_transform)
```

와 같이 datasets를 가져와 transform 포함해서 넣고,

```jsx
train_loader = DataLoader(train_ds, batch_size=batch_size, shuffle=True, num_workers=2)
test_loader = DataLoader(test_ds, batch_size=batch_size, shuffle=False, num_workers=2)
```

와 같이 dataloader에 넣어서 나중에 dataloader에서 for images, labels in ~로 batch를 하나씩 꺼내온다.

**model**

class ResidualBlock(nn.Module): 와 같이 nn.module을 상속받으면 기본적인 torch의 레이어 블록이 된다. 이 안에 __init __, forward만 구현해두면 backprop, 기타 처리를 알아서 다 해준다.

forward는,

```python
def forward(self, x):
        """
        forward pass 구현 (Residual blocks)
        """
        # Initial conv
        x = self.conv1(x))
        x = F.relu(self.bn1(self.conv1(x)))
        x = self.bn1(x)
        x = F.relu(x)
        return x
```

와 같이 이전 계층을 다음 계층 인자로 넣어서 연쇄시키며 구현. 저 conv1, bn1 등은 모두 nn.module 상속받아 이런 조작이 된다.

**train**

model.train()을 하면 model 안의 모든 계층들이 train=True로 설정, 훈련 모드가 된다.

```python
optimizer.zero_grad() # 이번 역전파 기울기 초기화
outputs = model(images)
loss = criterion(outputs, labels)
loss.backward() # 역전파
```

이런 식으로 돌리는게 기본.

model.eval()을 하면 train=False로 설정.

with torch.no_grad():로 기울기 계산, 역전파 안 함.

모델 체크포인트 저장은 아래와 같이.

```python
torch.save({
        'epoch': epoch,
        'model_state_dict': model.state_dict(),
        'optimizer_state_dict': optimizer.state_dict(),
    }, filepath)
```

# 문제
파이썬에서 병목이 생기는 이유는 파이썬에서 호출해 전달하는 과정에서 병목이 나오는 것. 이걸 해결하기 위해 여러 블록이 들어간 하나의 큰 블록을 .compile로 하나로 만들어, 내부적으로 파이썬 호출을 없애고 [[기초 cs/c++\|c++]], [[개발/cuda\|cuda]]로 돌리는 방법이 있다.