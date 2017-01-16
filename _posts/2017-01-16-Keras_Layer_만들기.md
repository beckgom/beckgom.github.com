---
layout: post
title: "Keras - 자체 layer 만들어 보기"
description: ""
category:
tags: [deep learning, keras]
---

# Keras Layer 만들기
만들 필요성이 생겨서 우선 찾아보게 되었다.

내용을 보자.

![](/assets/2017-01-16-Keras_Layer_%E1%84%86%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%86%AF%E1%84%80%E1%85%B5/614972BE-E59D-4F72-A033-B59BACA72227.png)

기본 제약 사항이 `keras==1.1.3` 이상이다. 요즘에는 1.2.0을 쓰니까 현재는 상관하지 않아도 될 것 같다.

기본 layer의 경우 아래 3가지 내용만 구현하면 된다고 한다.

#### `build(input_shape)` : 

기본적으로 weight를 정의해주는 곳이다. 실제로 코드를 보면 

```python
self.W = self.add_weight(shape=(), initializer='random_uniform', trainable=True)
```

형태로 되어 있다.

그리고 항상 `self.built = True` 를 삽입하거나 상속받아서 하는거니까 `super(class_name, self).build()` 로 대체도 가능하다.   
정리하면

```python
self.W = self.add_weight(shape=(), initializer='random_uniform', trainable=True)
super(class_name, self).build()
```

#### `call(x)` : 

실제로 실행하는 부분이다.  
매트릭스 연산을 하는 것으로 예를 들면 다음과 같다.  

```python
def call(self, x, mask=None):
  return K.dot(x, self.W)
```

K는 backend에서 가지고 오는 부분이고, mask 부분은 아직 뭐하는 부분인지 모르겠다.   
이 부분은 나중에 실제 코드 중에 None이 아닌 케이스 중에 어떻게 하는지 보는 것으로 해야겠다.

#### `get_output_shape_for(input_shape)` :

입력이 들어왔을 때, 나오는 출력의 shape이라고 보면 된다.  
실제로 matrix 연산이니까, 입력의 1차원과 출력 차원이라고 보면 된다.  
결과는   

```python
def get_output_shape_for(self, input_shape):
  return (input_shape[0], self.output_dim)
```

형태로 떨어진다.


### 예제로 Maxpooling을 짜보자.

간단한 layer인 maxpooling을 짜보자.   
간단하게 짤꺼니까 (2,2) 형태를 가지고 stride도 2인 경우로 보자.  

```python
class MaxPooling(Layer):
	def __init__(self, **kwargs):
		super(MaxPooling, self).__init__(**kwargs)

	def build(self, input_shape):
		super(MaxPooling, self).build()

	def call(x):
		return K.pool2d(x, (2, 2), strides=(2, 2), border_mode='valid', dim_ordering='default', pool_mode='max')

	def get_output_shape_for(self, input_shape):
		return (input_shape[0]/2, input_shape[1]/2)
```

맞는지 모르겠으나 얼추 이런식으로 하면 되겠다.   
기본적으로 call에 들어가는 operation은 [Backend - Keras Documentation](https://keras.io/backend/) 에 있는 function을 참고해서 사용하면 되겠다.   
왠만한 내용은 다 있는듯 하고,  
기존에 구현되어 있는 layer를 참고하면 충분히 할 수 있을 것으로 보인다.

다만 이건 layer를 받아올 때 사용하는 방식이고   
recurrent쪽은 recurrent라고 하는 core layer가 별도로 존재한다.   
이 부분은 나중에 따로 정리해보자.