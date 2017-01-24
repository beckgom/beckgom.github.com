---
layout: post
title: "Paper - Identity mappings in deep residual network"
description: ""
category:
tags: [deep learning, paper]
---
# Paper - Identity mappings in deep residual network
링크는 …

[1603.05027 Identity Mappings in Deep Residual Networks](https://arxiv.org/abs/1603.05027)

## 뭐하는 논문인지?
2015년인가? imagenet을 휩쓸었던 resnet 저자가 쓴 논문이다.  
실제로 내용을 보면 resnet에서 기본 모듈의 구조를 변경하였다.
어떻게 보면 큰 변경이 아닐 수 있는데,  
설명하는 부분들을 정리해서 보면 그 차이가 클 수 밖에(?) 없더라..  
라고 하는 논문이다.

## 수정점은?
기존의 모듈과 새로운 모듈의 차이는 아래 그림을 보면 알 수 있다.

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/853D5795-76D9-4A5D-9133-4B1F89F90045.png)


기존에는 addition을 한 다음에 relu를 했다면 

이번에는 입력에서 residual path 처음부터 activation 처리를 하고

합칠 때는 그냥 더하고 만다.

이게 사실 큰 차이가 아닐 수 있는데, 실제로 수식을 전개해보면 차이가 명확하다.

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/48EAA936-2326-4D3E-AA96-FE11715F24D3.png)

위의 식이 기본 꼴이고 $$h(x_l) = x_l$$ 인 identity mapping이다.

기존의 방식은 $$f(y_l)$$이 RELU였는데, 이걸 비틀어서 $$f(y_l) = y_l$$로 해보자는 거다.

이렇게 하면 이걸 쌓았을 때 장점이 생긴다.

우선 용어 자체는 `pre-activation`이라고 하는데, activation이 결국은 residual path로 들어가야하고 이 때문에 residual path 초기에서 activation 처리를 해주기 때문으로 해석하면 된다.

기존의 방식은 `post-activation`이라고 보면 되겠고…

이 방식으로 하면 상위 layer는 다음과 같이 표현 가능하다.

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/1CB94D3C-D70A-4449-90B1-DBB4FDC16D94.png)

그리고 여기에서 recursively로 보면 아래와 같이 표현 가능하다.

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/B0B97175-3507-4E4C-826E-97F7C9975CC5.png)

결국 

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/4FBC40F7-103D-45F3-954B-6B2889BD7CDA.png)

위와 같은 형식으로 표현이 가능하게 된다.

이걸 backward propagation의 관점으로 보면

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/47CCDEAD-D93B-4A8D-B616-171136B939F8.png)

위와 같이 표현이 가능해진다.  
즉, 2개의 텀인데 하나는 거의 상수 텀이 되고, 하나만 back을 탄다고 보면 되겠다.  
게다가 위의 식이 0이 되는 경우는 뒤의 summation term이 -1이 되어야 하는데, 항상 -1이 되는 경우는 발생하지 않는다.(?)  
그래서 결국은 뭐 좋다는 거지.

## 성능은?
![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/BBB06F9C-9A90-4B76-AE4F-2FA15ED1DC3A.png)

이 그림을 하나 보면 대충 내용이 다 나올 듯 싶다.  
정리하면 post-activation에서 pre-activation으로 가는 중간 과정에 대해서 다 실험을 해봤는데,  
마지막 방식이 제일 좋았더라..이런 내용 정도 되겠다.   
(c) 를 보면, relu를 안쪽으로 넣은건데, 이렇게 되면 residual 성분 자체가 항상 non-negative가 되어서 손실이 발생한다고 봄.  

다만 결과를 보면 (e)를 제외하곤 기존 방식보다 좋다고 볼 수 없다.   
실험을 하다가 ㅎㄷㄷ하지 않았을까? 싶었다.  


## 기타 실험 내용은?
identity mapping외에 다양한 종류에 대해서 실험을 해봤다.  
결국 자신들 방식이 좋을 수 밖에 없는걸 수식을 조금 이용해서 이야기 하고 있다.  
추가적인 실험을 한 결과도 마찬가지로 보이고…

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/7617B18E-81CE-4D46-ACA0-0FE2E35F85ED.png)

6가지에 대해서 하더라도 결국 original이 제일 좋다는 실험 결과.  
여기서보면 중간 2개는 highway network에서 제안한 방식임.

![](/assets/2017-01-24-Paper%20-%20Identity%20mappings%20in%20deep%20residual%20network/44D9B459-CF0F-4578-A1C0-4E68C375BD15.png)


## 기타 얻을만한 정보는?
훈련시간은 cifar에서는 1001 layer에서 2개 GPU 써서 27시간 정도 걸리는 것으로 결과를 보고 하고 있다.

Imagenet의 경우에는 200 layer에서 8개 써서 3주 (-_-a) 떱…

> 논문 내용을 보면 중간 중간 layer를 섞어서 실험했던 내용들을 깨알같이 이야기하고 있다. 그런 점에서 논문 자체적으로는 얻을만한 정보가 많다고 볼 수 있겠다.  


## 질문
* 맨 처음 입력부터 residual에 bn, relu를 적용하는 것인지?
	* 정확히는 모듈 시작하기 전에 conv layer가 하나 존재한다.
	* 그리고 depth가 바뀌는 부분들이 존재하는데 거기의 경우에는 1x1 conv로 결국 filtering하는 컨셉이다.
		* 보다 정확히는 projection이라는 용어를 쓴다.
	* 즉, identity mapping 에 해당하는 녀석이 맨마지막까지 완전히 identity로 쭈욱 아니고, 같은 모듈 안에서 처리하는 것이라고 보면 되겠음.
* 러닝레이트는? 
	* 맨 뒤에 detail에 적어놓은 것 봤더니 step-down 방식으로 처리함.
* skip connection
	* [Skip connection](bear://x-callback-url/open-note?id=90229FA9-DFAE-4C40-A9F2-B4AA0DDA5ACB-27241-000096B8D24295B0)
* 속도 대비로 성능이..?
	* 속도 생각하면 inception으로 하는 것이 좋지, 구지 depth를 막 늘려갈 필요가 있을까?
