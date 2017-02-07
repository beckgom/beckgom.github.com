---
layout: post
title: "Keras - LearningRateScheduler"
description: ""
category:
tags: [deep learning, keras]
---
# Keras - LearningRateScheduler
링크는 …  
[Using Learning Rate Schedules for Deep Learning Models in Python with Keras - Machine Learning Mastery](http://machinelearningmastery.com/using-learning-rate-schedules-deep-learning-models-python-keras/)

## learning rate에 step down을 적용해보자.
digit을 쓰다보면 기본적으로 step down을 지원하는데, keras에서는 이러한 부분이 없다.  
그럼에도 Callback func을 통해서 구현이 가능하다.

방식은 다음과 같다.

## Source code
```python
from keras.callbacks import LearningRateScheduler

# learning rate schedule
def step_decay(epoch):
	initial_lrate = 0.1
	drop = 0.5
	epochs_drop = 10.0
	lrate = initial_lrate * math.pow(drop, math.floor((1+epoch)/epochs_drop))
	return lrate

lrate = LearningRateScheduler(step_decay)
callbacks_list = [lrate]
# Fit the model
model.fit(X, Y, validation_split=0.33, nb_epoch=50, batch_size=28, callbacks=callbacks_list)
```

## 해설
기본적으로 LearningRateScheduler라는 callback func이 존재하고, 거기에 붙여 넣을 func을 정의해주면 된다.  
다만   

https://keras.io/callbacks/#learningratescheduler

에 나와있는 것에 따르면, func는 입력으로 epoch를 받을 것이고, 출력으로 그에 해당하는 learning rate을 출력하면 된다.  
다만 위의 예제에 따르면 현재  learning rate을 받아오지 못하기 때문에, optimizer에 설정한 lr은 사실상 의미없게 되버린다.  
…  
…  

뭐 방법이 있겠지, 나중에 함 찾아봐야겠다.

그리고 저 방식을 할 경우, learning rate decay 설정등의 내용을 사용할 수 없게 된다.  
게다가 adam에다가 저걸 적용해도 여전히 써보면 장점보다는 단점이 더 있는 것 같고…  
learning rate decay 등을 사용하면 구지 쓸 필요가 없을 수 있겠다는 생각이 들었다.

