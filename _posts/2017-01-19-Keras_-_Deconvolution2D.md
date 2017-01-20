---
layout: post
title: "Keras - Deconvolution2D"
description: ""
category:
tags: [deep learning, keras]
---

# Keras - Deconvolution2D
링크는…

[Convolutional Layers - Keras Documentation](https://keras.io/layers/convolutional/#deconvolution2d)

딥러닝을 이용한 segmentation 연구를 보면 FCN 도 그렇고 포스텍 연구도 deconvolution을 사용한다.

어떤 케이스에서는 convolution을 그대로 사용하는 경우들도 있기는 하나, 뭐 있으니 한번 알아보자.

## 기본 폼
```python
keras.layers.convolutional.Deconvolution2D(nb_filter, nb_row, nb_col, output_shape, init='glorot_uniform', activation=None, weights=None, border_mode='valid', subsample=(1, 1), dim_ordering='default', W_regularizer=None, b_regularizer=None, activity_regularizer=None, W_constraint=None, b_constraint=None, bias=True)
```


대부분은 convolution과 유사하다.  
다만 달라지는 부분만 좀 알아보려고 한다.

## Arguments

![](/assets/2017-01-19-Keras_-_Deconvolution2D/51B574F0-EB61-440C-BA5A-534DE9CC59C4.png)

대부분은 convolution과 같다.   
관련 링크는…

아직 없다.

다른 부분은,  

* output_shape:
	* (nb_sample, nb_filter, nb_output_rows, nb_output_cols)의 튜플 방식으로 사용한다. 이거를 계산하는 수식이 있는데 다음과 같다.
	$$o = s (i - 1) + a + k - 2p, \quad a \in {0, \ldots, s - 1}$$

	
## 정리

다음에는 unpooling 를 한번 정리해야겠다.  
그러면 segmentation 쓸 내용은 다 보는 격..
