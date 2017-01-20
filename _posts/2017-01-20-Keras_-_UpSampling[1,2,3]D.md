---
layout: post
title: "Keras - UpSampling[1,2,3]D"
description: ""
category:
tags: [deep learning, keras]
---

# Keras - UpSampling[1,2,3]D
링크는 …

[Convolutional Layers - Keras Documentation](https://keras.io/layers/convolutional/#upsampling2d)

보통 segmentation할 때 많이 사용하는 upsampling이다.  
오디오나 음성에서의 upsampling처럼 뭔가 내부적으로 필터링을 하거나 이런건 **없다**  
그냥, `값을 그대로 반복해서 쓴다`

## 기본 폼
```python
keras.layers.convolutional.UpSampling2D(size=(2, 2), dim_ordering='default')
```

아, 오랜만에 심플한 layer다. 

좋다!!

기능 자체가 간단할 뿐만 아니라, 뭐…생각해보면 argument도 받을게 딱히 없긴 하다.

## Arguments
![](/assets/2017-01-20-Keras_-_UpSampling%5B1,2,3%5DD/54ACD8FD-5701-4D6E-A8B7-E4D9BCD4C405.png)

역대 가장 간단한 argument!!

* size:
	* tuple 형태로 받는다. 물론 지금은 2D 기준이니까 그렇고 1D 면 그냥 int로..
* dim_ordering:
	* 2d, 3d에만 해당한다. `th`와 `tf`의 ordering이 달라서 그런거고, `keras.json`에 명시된대로 하는 것이 `default`이다. 이걸 구지 바꿀 일이 있을까 싶지만, 뭐 argument로는 빠져나와 있다.

## 정리
정리라 할 것도 없기 매우 간단한 layer다. 이것까지 연결하면 segment에 바로 적용이 가능할 것으로 보인다.

끝!	
