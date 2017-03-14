---
layout: post
title: "Paper - Matching network for one shot learning"
description: ""
category:
tags: [deep learning, paper]
---


## One shot learning?
말그대로 하나만 딱 돌려서 클래스에 대한 분류를 완성한다는 의미이다.  
조금은 큰 범위로 봐서 클래스별 1장이 아니라 5장이나 소수의 몇 장 정도로 이야기하기도 한다.  

## 본 논문은?
one shot learning을 하는데 있어서 필요한 extractor (feature extractor)를 neural network로 하겠다는 취지다.  
다양한 one shot learning 기법들이 있긴한데, 여기서는 extractor를 matching network라는 이름으로 정의하고,  
그에 대한 내용을 설명하고 있다고 보면 되겠다.

## 목차
1. Introduction
2. Model
	1. Abstract explanation
3. ~~Related work~~
4. Experiments
	1. Omniglot
	2. ImageNet (modified)
	3. ~~Language model~~
5. Conclusion
6. Appendix
	1. Model in detail


## Intro
One shot learning에 어울리는 기존 방식은?
-> nearest neighbors (kNN)

MANN, metric learning도 있음. (자세한 설명은 3장)

* matching networks	
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/EAD5563E-0B4A-4263-929A-9D92B5C0EDBA.png)
$$f_{\theta}$$와 $$g_{\theta}$$를 이용하여 가장 적합한 클래스를 찾는 것


## Notation
$$x, y$$ : 훈련에 사용한 클래스의 입력과 그의 label  
$$\hat{x}, \hat{y}$$ : 훈련에 사용하지 않은 클래스의 입력과 그의 label  
$$S$$: 훈련에 사용하는 데이터셋의 집합  
$$S`$$: 훈련에 사용하지 않는 데이터셋의 집합  
$$B$$: 훈련에 사용하는 데이터셋의 batch-set  
$$k$$: 훈련에 사용하는 클래스의 수  
$$c()$$: cosine similarity function  

## 전체적으로 돌아가는 방법
1. Training set을 구성한다.
2. Training set으로 부터 support set $$S$$과 batch set을 생성한다.
	![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/B892DB35-D632-4184-965B-1F24F995E5E0.png)
3. Training 진행!!! $$\theta$$ 훈련
4. Support set $$S$$과 새로운 (테스트에 사용할) support set $$S’$$을 구성한다.
5. 새로 구성한 support set, $$S’$$으로 $$\hat{y}$$를 만든다.
	![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/CDDFBD86-5A6D-47E0-8E75-6E4C1A510A84.png)
6. $$\hat{y}$$으로 정답과 비교한다.
7. 끝


## Model architecture
메모리에 저장하는 것과 유사하게 $$S$$에서 만든 정보를 이용하여 one shot learning에 활용

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/4BC9D7B0-293F-4BDB-A97A-C0EABCA26A07.png)

여기서 $$a()$$는 attention kernel임. 정의는 

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/C38B6362-8AE4-481F-A719-75A02ADCEA45.png)

softmax + cosine similarity + feature extractor 정도로 표현 가능

$$\hat{y}$$가 나오고 나면, 그 다음부터는  label과 맞춰보면 끝.  

여기까지만 보면 neural network하고 연관성은 전혀 없다.

## Full Context Embeddings
appendix에서는 fully conditional embedding이라는 이름으로 -_- 나옴  

`$$f(x)$$와 $$g(x)$$를 neural network으로 구성해보자!`

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/F4572320-3305-4D80-A97F-731A0D323A9F.png)
LSTM을 포함한 특이 구조

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/4FE37246-A46B-47D0-9CAA-8AC566F548A1.png)
BLSTM + skip connection구조임

여기서 $$f’(x)$$와 $$g’(x)$$는 입력에 따른 1차 feature extractor라고 보면 된다.  
이미지의 경우 CNN에서 softmax만 뺀 상태에서 벡터열을 가지고 옴

## In detail
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/88F957E0-C42E-4FF8-AACD-1C78C7E8C162.png)

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/A65586AF-8039-4F2A-B7A0-E534B4B54E60.png)


## Training Strategy
Objective function은 다음과 같이 구성함

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/7FCD2612-1279-41C9-8395-1135DBBA4BE1.png)
$$P_{\theta}()$$는 기존의 classification을 구하는 방식과 동일하다고 보면 됨


## FCE in Image
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/E82FD213-CF7C-4E75-9D93-4718C442939A.png)

## FCE $$g$$
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/E50C76D4-F6C7-4688-B9C6-62EDFEA8B3D8.png)

## FCE $$f$$
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/BECCCC21-7D7B-467E-8864-684E3FDCF03E.png)

## Experiments
### Omniglot

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/B055524F-C311-4BC2-91A6-62150F581498.png)

1623개 문자 (각 20개씩..)
one shot learning에 적합한 Database

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/1E58ABE6-10DA-487C-933B-6B98791DFC09.png)


### ImageNet
전체를 다쓰진 않고 random으로 118를 지운 것을 training으로 쓰고 118개를 테스트로  
-> randImageNet

dogs만 지우고 (118) traing, dogs는 테스트로만  
-> dogsImageNet

자체적으로 사이즈 줄이고 100개 클래스만 모아서 쓴거 (train/test=80/20)  
-> miniImageNet


![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/6B340752-2E76-4AFA-964C-CC5E05CA9EBB.png)
![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/83B2B85B-5A95-4810-B76D-B1382BE76E3B.png)

![](/assets/2017-03-13-Paper_-_Matching_network_for_one_shot_learning/533CACC1-1785-440F-ACA1-23F301FD3927.png)


## Conclusion
end-to-end one shot learning  
**Differentiable** nearest neighbor   

장점으로는..  
성능도 일반 classifier를 쓰는 것보다는 더 향상됨  
빠르게 학습 가능함  

단점으로는..  
 클래스가 많아지면 느려짐..  
kapathy’s blog에 언급처럼 비교대상에 대한 확인이 필요함  
FCE 적용시 더 나빠지는 경우도 있음 (Omniglot)  
hyper-parameter 로 되어 있는 tstep에 따라서 성능이 차이남(예상)  


## References
[1606.04080 Matching Networks for One Shot Learning](https://arxiv.org/abs/1606.04080)
[Matching networks for one shot learning](https://www.slideshare.net/KazukiFujikawa/matching-networks-for-one-shot-learning-71257100)
[paper-notes/matching_networks.md at master · karpathy/paper-notes · GitHub](https://github.com/karpathy/paper-notes/blob/master/matching_networks.md)
[GitHub - zergylord/oneshot](https://github.com/zergylord/oneshot)



