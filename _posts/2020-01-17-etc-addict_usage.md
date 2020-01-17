---
layout: post
title: "뭘 하나 써도 조금 더 잘 쓰자. - addict"
description: ""
category:
tags: [etc]
---

## addict??

`addict`, 크\~ 이름 한번 잘 지었다 생각이 들었다.  
뭔가 중의적이라는 점 때문이다. 정확한 뜻에 비춰보면,  
advanced dict 정도 될듯 싶다. python 내에 dict가 있는데 이걸 조금은, 
쿼리 형식처럼 쓸 수 있다는 것이 장점이다.

```python
from addict import Dict

original_dict = dict()
original_dict['name'] = "John Doe"
original_dict['age'] = 20

advanced_dict = Dict(original_dict)
print(advanced_dict.name)
# John Doe
print(advanced_dict['age'])
# 20
advanced_dict.gender = "M"
```

위의 예제만으로도 충분히 어떤 역할을 하는지는 쉽게 알 수 있다.


## 언제 쓰면 좋을까?
원래 목적처럼 쿼리 형태처럼 쓰는데 활용해도 좋고,  
개인적으로는 hyperparameter를 parsing해서 쓸 때, JSON을 addict로 받아서 쓰면 참 괜찮은 것 같다.  
args. 처럼 쓸 수 있기도 하고, 계속 ['name'] 이런식으로 쓰는것보다는 폼도 나고 :)



## 어떻게 변형해서 쓰면 더 좋을까?
hp 방식으로 쓸때는, 한번 더 Wrapping해주면 좋은데, key가 존재하지 않는 경우에 대해서 처리를 해주는 것이 좋다.  
아주 코드를 매우 오타 없이 잘짜면 괜찮은데, 버그도 버그지만, 타이포로 문제가 생기는 경우들도 있어서...  
그 부분에 대한 처리를 사전에 해줄 수 있도록 수정하면 금상첨화  


## 가장 좋기는 개발 Framework에 포함시키기

지금 실제 하고 있는 작업이기도 한데 범용으로 실험에 활용할 수 있는 자체 framework(이라고 하기엔 조금 민망하지만..)  
Template화 시키는 작업을 하고 있다. 이것만 해도 사실 초반에 접근할 때 쉽게 할 수 있으니까 :)

그런 관점에서 활용하기 아주 좋은 package이다.