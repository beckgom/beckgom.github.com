---
layout: post
title: "Keras - Recurrent layer"
description: ""
category:
tags: [deep learning, keras]
---
# Keras  - Recurrent layer

언제나 처럼, 링크는 여기에…

[Recurrent Layers - Keras Documentation](https://keras.io/layers/recurrent/)

이미 자주 쓰고 있긴 하지만, 그래도 한번 정리하자.

## 기본 모습
```python
keras.layers.recurrent.Recurrent(weights=None, return_sequences=False, go_backwards=False, stateful=False, unroll=False, consume_less='cpu', input_dim=None, input_length=None)
```

위와 같은 모습으로 되어 있는데, 저 녀석 (`Recurrent`)은 parents class이다. 

그리고 저 녀석을 그대로 사용하진 못하고 `child class`인 `SimpleRNN, LSTM, GRU`를 사용해야 한다.




## Arguments
![](/assets/Keras_-_Recurrent_layer/D276F17D-5DE2-4C9B-873E-63D1C7676443.png)

좀 길다;;;;;;

하나 하나 보자.

* weight
	* 출력 weight에 대한 사이즈를 설정함. 3가지 방식이 가능하나, 맨 마지막 방식을 사용하면 됨.
* return_sequences
	* 결과가 many가 나오도록 하는 option이다. 이게 False로 된다면 one으로 나가는 것이 됨
* go_backwards
	* 입력을 반대로 하는 것과 동일한 효과이다.
* stateful
	* default는 `False`인데, `True`가 되면 다음 batch에 첫 임력을 이전 batch의 hidden을 사용할 수 있도록 함. 이 부분은 나중에 이미지 캡셔닝의 inferene쪽에서 사용할 수 있음. batch 샘플별로 hidden을 사용함. batch 내부에서 하는건 아니고..
* unroll
	* Tensorflow에서는 항상 unroll이 되어 있는 상황이고,  th에서는 True로 설정을 하면 실제 속도면에서 올라가게 된다. 다만 short sequence에서 적당하다고 하는데, 다만 얼마나 short sequence라는 설명이 없다. ;; 떱.
* consume_less
	* default는 `cpu`로 되어 있는데  cpu에 적합하게 갯수 좀 줄이고 처리한다. 다만 메모리를 많이 잡는 다는 점이 단점.  `mem`으로 설정하면 메모리 적게 잡고 처리함 GPU에서를 확실히 빨라진다고 함. `gpu`는 LSTM/GRU에서만 동작을 하는데 gate 다 묶어서 처리하는 것으로 되어 있음. gpu에 적합하게 돌아감.
* input_dim
	* 첫 layer일 때 사용하는 것이고 input_shape으로 대체 가능하다.
* input_length
	* default는 `None`. 이게 tstep 때문에 3차원 데이터가 되는데, 앞에서 flatten이 되었다가 다시 3차원으로 되야 할 때 사용하는 것이 좋다.

## 정리	
기본적으로 설정해야하는 것들은 다음과 같다.

> weight, consume_less  

보통 `consume_less`에 대해서 사용하지 않는데,   
그럼 기본적으로 느리게 돌 수 밖에 없다. 이걸 바꾸면 빨리 좀 돌듯..  
실제로 돌려보면 30% 정도의 성능 향상이 있다.   
이 부분은 batch 사이즈를 늘림에 따라서 성능 향상이 크게 나타날 수 있을 것으로 보인다.  




