---
layout: post
title: "Keras - Functional API"
description: ""
category:
tags: [deep learning, keras]
---

# Keras - Functional API
링크는 …  
https://keras.io/getting-started/functional-api-guide/

## Sequential model & Functional API
keras에는 두가지 방식의 모델 생성이 가능하다.  
그것이 `sequential model` 과 `functional API` 이다.   
두가지 모두 알아두면 정말 도움이 된다.  
먼저 직관적이면서 쉬운 것은 sequential model 이고,  
조금 더 복잡하게 쓰고 싶을 때 funtional api를 사용하면 되겠다.  

### Sequential model
`torch`와 비슷한 형태로 사용한다.  
`:add(~~)` 방식이 `.add(~~)`로 바뀐 정도?  
바뀌었다고 하기도 민망할정도다.  
torch가 편한 부분이 있었는데 그대로 사용가능하다.  
물론 torch도 다르게 사용할 수 있다.  

예제 역시 직관적이다.

```python
from keras.layers import Merge

left_branch = Sequential()
left_branch.add(Dense(32, input_dim=784))

right_branch = Sequential()
right_branch.add(Dense(32, input_dim=784))

merged = Merge([left_branch, right_branch], mode='concat')

final_model = Sequential()
final_model.add(merged)
final_model.add(Dense(10, activation='softmax'))
```

그나마 복잡하게 사용한 것이 위의 예제이다.  
merge를 위해서 모델을 여러개 생성한 것인데,  
보면 알겠지만 간단하게 구현 가능하지만, 조금 복잡한 구조로 갈수록,  
형태가 길어질 수 밖에 없다.

### Functional API

페이지 첫 문장을 보면 보다 복잡한 모델을 만들 때 사용하라고 추천하고 있다.   
그러면서 그 다음 단락에서,  `sequential model`이 더 나을껄? 이라는 표현을 …;;

```python
from keras.layers import Input, Dense
from keras.models import Model

# this returns a tensor
inputs = Input(shape=(784,))

# a layer instance is callable on a tensor, and returns a tensor
x = Dense(64, activation='relu')(inputs)
x = Dense(64, activation='relu')(x)
predictions = Dense(10, activation='softmax')(x)

# this creates a model that includes
# the Input layer and three Dense layers
model = Model(input=inputs, output=predictions)
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
model.fit(data, labels)  # starts training
```

모양새를 보면 알겠지만 모든 기능을 함수로 표기한다. (이름 그대로..)  
이렇게 하면 장점이 있다. 바로 바로,  

기본 기능의 함수들을 묶어서 custom block을 만들 수 있다는 것!!  
물론 custom layer와는 다르다. 

예제를 보기 좋은 코드는 단연 resnet이다.    
[keras-resnet/resnet.py at master · raghakot/keras-resnet · GitHub](https://github.com/raghakot/keras-resnet/blob/master/resnet.py)

이중에 일부만 따오면, 

```python
def _bn_relu(input):
    """Helper to build a BN -> relu block
    """
    norm = BatchNormalization(mode=0, axis=CHANNEL_AXIS)(input)
    return Activation("relu")(norm)
```

와 같다. 이렇게 되면 중복되는 block은 간단하게 정리가 가능해진다.
resnet도 몇개의 block을 정의만 하면 간단하게 구현 가능해진다는 점!!!  
이 functional API의 장점이다.

처음에는 왜 이름이 functional API일까 생각했는데,  
막상 써보니까 이처럼 잘 지은 이름이 없다!

## 정리
모델을 조금 복잡하게 가지고 갈 필요가 있어서 사용하다가 정리하였다.  
다른 것보다 블럭화하여 사용할 수 있다는 점이 가장 큰 장점이라고 할 수 있겠고,  
중간 중간 수정할 때, 블럭화로 인해 인간 오류의 가능성이 줄어든다는 점에서 더욱 나에겐 쓸만하다.  

이제 실제로 layer만 따로 만들어보면 관련된 내용은 거의 다 활용해보는 것이 아닐까 싶다.

