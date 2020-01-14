---
layout: post
title: "뭘 하나 써도 조금 더 잘 쓰자. - tqdm"
description: ""
category:
tags: [etc]
---

## tqdm 의 장점

`tqdm`은 loop를 많이 돌려서 실험을 하는 경우에 매우 유용한 패키지이다.

<img src="http://beckgom.github.io/assets/2020-01-14/tqdm.png" width="640">

얼마나 남았는지도 잘 알 수 있고, 어느정도 속도로 얼마나 시간이 남았는지 알 수 있으니까 이것만으로도 매우 훌륭하게 사용할 수 있다.



## 근데 안썼던 이유
그런데 실험을 하다보면 중간에 실험 결과를 죽죽 확인하면서 보고 싶은 경우가 많다.  
예를 들면 중간 loss나 acc를 보고 싶은데 이걸 출력하기 시작하면 bar가 틀어지기 시작한다. 
그러다보니 print에 들어가는 내용에 total, iter 등을 포함시켜서 계속 print-out하게끔 해서 사용하고 있었는데, 
이게 보는데 큰 불편이 없기도 할 수 있는데 tmux를 쓰다보니까 그냥 스크롤이 안먹히는 점 등, 이래저래 불편함이 있긴했지만,
그래도 정보를 보는 것이 더 중요했던터라, 그렇게 사용하고 있었다.

## 역시 배워야 함. 방법은 다 있음
근데, 사람은 역시 배워야 한다고... 내가 불편하면 남들도 불편했을 것이고, 대부분은 누군가 해결방법을 만들어 놨다는 점을 망각하고 있었다.  
tqdm에 이미 관련된 내용을 지원하는 내용이 있더라...  
메뉴얼 따위 안읽는 자의 최후...정도 되겠지...  

```python
import tqdm

train_loader = tqdm.tqdm(train_dataset, desc='Loading train dataset')
for i, x in enumerate(train_loader):
	...
	...

	train_loader.set_description("Loss %.04f Acc %.04f | step %d" % (loss, acc, i))

```


## 하나하나 이렇게라도 정리해서 잘 쓰자.
실제 잘 쓰는 툴임에도, 정확히는 잘 쓰고 있다고 생각하는 많은 툴임에 대해서도 여전히 공부해야할 것이 많음을 느낀다.   
tqdm만 해도 jupyter notebook에서 쓸 때 어떻게 써야하는지,  
Hook은 어떻게 걸고 쓰는지 등 공부할 것이 너무 많다.  
하나하나 이렇게 기회 났을 때 정리해두면,  
나중에 더 잘 쓰겠거니... 싶으니...  앞으로도 정리해보자.