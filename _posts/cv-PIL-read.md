---
title:  CV/PIL读取图片踩坑记录
date: 2023-11-11 18:25:57
categories:
    - AI_learning
    - Technology
---
啥也不说了直接上代码（）

```python
import cv2
import torch
from torchvision import transforms
from PIL import Image
path = './archive\imagesTr\CHNCXR_0640_1.png'

data_transforms = {
        "train": transforms.Compose([
            transforms.ToTensor()
            ]),
        "test":transforms.Compose([
            transforms.ToTensor()
            ])
    }

img = cv2.imread(path, cv2.IMREAD_GRAYSCALE)
print(img.shape)
img = data_transforms["test"](img)
print(img.shape)
# img = torch.from_numpy(img)

label = Image.open(path).convert("L")
label = data_transforms["test"](label)
print(label.shape)
```