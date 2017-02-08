---
layout: post
title: "Keras - BatchNormalization() 속도"
description: ""
category:
tags: [deep learning, keras]
---
# Keras_-_BatchNormalization()_속도
## BatchNormalization()이란..
잘 정리된 내용은 …
[batch normalization 설명](https://shuuki4.wordpress.com/2016/01/13/batch-normalization-설명-및-구현/)

간략히 정리하면,

> layer 입력별 whitening을 하는 것  

이라고 볼 수 있겠다.  
너무 퉁 친 내용이라고 볼 수 있을텐데, 실제로 내용은 무지 길다.  
그럼에도 사용하는데는 큰 지식을 필요로 하지 않기 때문에 위의 링크를 참고하도록 하자.

## Keras에 구현된 BatchNormalization()
keras에 보면 batch normalization이 구현되어 있다.  
링크는.. 
[keras - batch normalization](https://keras.io/layers/normalization/)

```python
keras.layers.normalization.BatchNormalization(epsilon=0.001, mode=0, axis=-1, momentum=0.99, weights=None, beta_init='zero', gamma_init='one', gamma_regularizer=None, beta_regularizer=None)
```

![](/assets/2017-02-08-Keras-BatchNormalization()_%E1%84%89%E1%85%A9%E1%86%A8%E1%84%83%E1%85%A9/3157177D-8ED3-45EB-92B6-F08F1D5CB00D.png)

argument는 여러가지가 있지만 일반적으로 따로 설정하지 않고 사용해도 무방하다.   
default는 feature wise norm으로 되어 있다.

꽤 오래된 구현 내용이기도 하거니와,  
최근에는 많이 쓰는 부분이라서,  
당연하게 존재한다. 다만..

## 속도 문제
속도 문제가 존재한다. -_-;  
특히 theano backend를 할 경우, 매우 느려지는 경우가 왕왕있는데,  
아직 해결안된 듯하다.
tensorflow에서는 크게 느려지진 않는 것 같지만,  
개인적으로 현재 돌리고 있는 model에서는 10배 가까운 속도 저하가 발생하였다.  
tensorflow용으로 backend를 바꾸자니, deconv에서 output shape에 대한 설정이 바뀌어야 하는 듯하다 ㅠ.ㅠ  


## 고민
우선은 BN을 사용하지 않더라도 조금 수정이 필요한 상태이기 때문에 현재는  
BN을 뺀 상태에서 개발을 하고 있다. 다만, 나중에는 조금이라도 성능을 올리기 위해서 BN을 사용할 필요가 있을텐데,  
어떻게 될런지 고민이다.  
tensorflow 에서 하더라도 deconv 설정을 바꾸는 문제가 있고, 
최신 tensorflow를 사용하자니 cuda 8.0이 필요한데, 이렇게 되면 docker server/client 둘다 올리면서 드라이버 건드려야 하고 등등 ㅠ.ㅠ  
피곤한 일이 매우 많아진다.   
이번 기회에 서버 하나 꾸릴 일이 있으면 좋겠다 싶다. ㅠ.ㅠ

