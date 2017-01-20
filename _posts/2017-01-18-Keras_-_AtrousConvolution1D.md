---
layout: post
title: "Keras - AtrousConvolution1D"
description: ""
category:
tags: [deep learning, keras]
---

# Keras - AtrousConvolution1D
링크는…

[Convolutional Layers - Keras Documentation](https://keras.io/layers/convolutional/)

이름이 생소한 편이다. atrous라니…

근데 다른 이름이 `dilated convolution`이다.

그렇다.

`wavenet`에서 사용하는 그것이다.

[WaveNet: A Generative Model for Raw Audio | DeepMind](https://deepmind.com/blog/wavenet-generative-model-raw-audio/)

그럼 한번 살펴보자.


## 기본 폼
```python
keras.layers.convolutional.AtrousConvolution1D(nb_filter, filter_length, init='glorot_uniform', activation=None, weights=None, border_mode='valid', subsample_length=1, atrous_rate=1, W_regularizer=None, b_regularizer=None, activity_regularizer=None, W_constraint=None, b_constraint=None, bias=True)
```

뭐가 엄청 많다.   
자세한 내용은 arguement에서 보자

## Arguments
![](/assets/2017-01-18-Keras_-_AtrousConvolution1D/8A9FEDA5-9F04-4D56-A199-A0EFFA85EF4A.png)

하아. 많다. 

하나 하나 봐보자.

* nb_filter:
	* feature map 갯수로 보면 되겠다.
* filter_length:
	* 1d니까 int 숫자로 표현
* init:
	* 초기값 설정 (따로 안만져도 될듯..)
* activation
	* 이건 알지?
* weight
	* embedded 처럼 기존의 훈련된 것 있으면 가져다가 쓸 수 있음.
* border_mod:
	* convolution이니까 필요함. `same` 이면 동일한 사이즈로 나온다.
* subsample_length:
	* subsamplong (downsampling)을 내부적으로 사용할 때 필요.
	* pooling의 1차원 version인 것 같은데 그냥 빼지않고 뭔 처리를 하나?
* atrous_rate:
	* `filter_dilation`이라고 볼 수 있을 테고, 결국 얼마나 건너뛸지 정도겠다. 즉, `filter_length`를 넘어갈 수 없을듯..
* W_regularizer:
	* [Regularizers - Keras Documentation](https://keras.io/regularizers/)
	* regularization을 하고 싶을 때 걸 수 있는 옵션. `ㅣ2`등으로 설정해서 사용할 수 있다.
* b_regularizer:
	* ``W_regularizer`의 bias용
* activity_regularizer:
	* 잘 모르겠다.
* W_constraint:
	* [Constraints - Keras Documentation](https://keras.io/constraints/)
	* weight에 대해서 constratint를 하나 걸 수 있다. 비음수나 unitnorm등이 가능
* b_constraint:
	* `W_constraint`의 bias용
* bias:
	* bias를 쓸지 말지
* input_dim:
	* `input_shape`과 동일한 term
* input_length:
	* [Keras - Recurrent layer | beckgom’s fabular](http://beckgom.github.io/2017/01/17/Keras_-_Recurrent_layer.html)의 ` input_length`와 동일한 의미


## 정리

생각보다 정말 많다. @.@

그래도 최소한으로 설정해서 볼 것들은 다음과 같다.

> nb_filter, filter_length, border_mode, atrous_rate  

이정도는 반드시 설정이 필요한 부분이고,  
나머지는 필요에 따라서 설정하고 쓰면 될 것으로 보인다.

휴..

~~생각보다 많아서 힘들었네;~~
