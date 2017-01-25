---
layout: post
title: "Keras - Reshape & Permute layer"
description: ""
category:
tags: [deep learning, paper]
---
# Keras - Reshape & Permute layer
링크는 …
[Core Layers - Keras Documentation](https://keras.io/layers/core/#reshape)

auto-encoder와 다르게 segmentation은 결국 x,y (or z) 좌표에 대해서 각각 class를 비교해야한다.  
즉, on/off라고 하면 image size가 on/off용 각각 1장씩 총 2장 (depth)만큼 필요하게 된다.  
그래서 (row, col)로 되어 있는 녀석을 serialize해야한다.  
그래야 각 point (pixel)별 softmax 처리를 통해서 class 를 판단할 수 있기 때문이다.  
이 과정에서 필요한 layer가 `reshape`과 `permute` layer이다.

## Reshape layer

```python
keras.layers.core.Reshape(target_shape)
```

argument를 따로 설명할 것도 크게 없을 만큼 간단하다.  
numpy 의 reshape을 사용했었다면 더욱 쉽게 이해할 수 있다.   

다만,  
np.reshape에서 지원하는 `-1`에 대한 기능을 사용할 수 없다.   

예를 들어,  
(3, 16, 16) 을 serialize한다고 하면 np.reshape에서는 (3, -1)로 써주면 알아서    
뒤에 크기가 결정되었는데, 여기선 직접 계산해서 작성해주어야 한다.  
즉, Reshape((3,256)) 으로 작성해야만 정상적으로 동작한다.  

이 부분만 주의하면 되겠다.

## Permute layer

```python
keras.layers.core.Permute(dims)
```

축을 변경할 때 필요한 layer이다.   
사실, inference할 때는 필요 없을 법한 layer이긴 하다. (물론 reshape도 마찬가지)  
다만 softmax로 해서 처리할 때는 맨 하위 축이 class 를 담고 있어야 한다.   

따라서 일반적으로 permute 처리를 해주어야 한다.  
만약 `th` ordering을 사용하고 있었다면 안해줘도 될 것 같다.  

물론 model 안에서 reshape, permute layer를 사용했으니까 label도 그에 맞도록 수정해주어야 한다.

