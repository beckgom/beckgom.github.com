---
layout: post
title: "Keras - Callback:ModelCheckpoint"
description: ""
category:
tags: [deep learning, keras]
---

링크는…  
[ModelCheckpoint - Keras](https://keras.io/callbacks/#modelcheckpoint)

Keras 뿐만 아니라, epoch을 많이 돌다보면 중간 결과가 더 좋을 경우들이 있다.  
즉, 맨 마지막에서 local minima에 빠져서 마지막에 결과를 저장해서는 성능이 좋지 않은 경우가 더러 있다.  
이러한 경우를 위해서 일정 epoch가 지나면 결과를 저장하는 방식 등 다양한 방법들이 있는데,  
그 역할을 하는 방법이 keras에서는 ModelCheckpoint를 사용하는 것이다.

## 기본 폼
```python
keras.callbacks.ModelCheckpoint(filepath, monitor='val_loss', verbose=0, save_best_only=False, save_weights_only=False, mode='auto', period=1)
```

## Argument
![](/assets/2017-02-10-Keras_-_Callback_ModelCheckpoint/8C881795-4C44-404D-A378-19EE13C87BB4.png)

반드시 넣어야 하는 것은 filepath 이다.  
`save_best_only`를 `True`로 설정할 경우에는 그냥 파일명을 정하면 되지만,  
그 외에는 다음과 같은 방식으로 이름을 정해야 한다.  
`weights.{epoch:02d}-{val_loss:.2f}.hdf5` 로 해놓으면 epoch, val이 값으로 삽입되어  
여러 모델을 다른 모델명으로 가능하다.  

## 정리
이 방식이 좋기는 하다.   
아직도 learning rate 출력이 어렵긴 하지만 쓰면 쓸수록 keras가 참 쉽게 잘 만들었다는 생각이 든다.

굿~!