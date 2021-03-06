---
layout: post
title: "Deep learning의 세계"
description: ""
category:
tags: [DNN]
---

## Deep learning
요즘, 기회가 되면 최근 이슈가 되고 있는 기술을 찾아보기도 하고 읽어보기도 하고 그런다.
그러다가 정말 관심이 가면, 그걸 실제로 돌려보기도 하고..  
물론 돌려보기 위해서는 부가적으로 해야할 일이 매우 많지만, 그래도 운이 좋으면 돌릴 수 있는 기회를 얻는다.


## 이제 이런 것까지?
오늘은 유투브에서 신기한 영상을 봤다.  
사진을 넣고 어떤 그림의 터치가 두드러진 사진(예를 들면 반고흐의 별이 빛나는 밤에)을 넣으면,  
반고흐가 그린 것같이 리터칭되어 사진이 리턴된다. @.@

이러한 작업은 왠지 이미지 도메인 지식이 있어야 처리할 수 있을 것 같지만,  
deep learning과 함께라면..(?) 그럴 필요도 없다.

샘플 사진은 다음과 같다.  
먼저 원본이 아래와 같다면  
![원본](/assets/mt.jpg)

아래와 같은 사진들이 생성 가능하다.

![이미지1](/assets/picasso.jpg)
![이미지1](/assets/seated.jpg)
![이미지1](/assets/starry_night.jpg)
![이미지1](/assets/style.jpg)

다른 것들도 돌려보면 세밀한 것까지 바라긴 어렵지만 그래도 분위기를 충분히 낼 수 있다는 점에서  
놀랍다고 할 수 있겠다.

## 생각해보면 정말 간단(?)한데
아이디어만 보면 천재적으로 간단하다. `피쳐를 뽑을 때는 터치에 대한 그림을 쓰고, 그걸 이용해서 다시 만들고`  
CNN 관점에서 보면 더욱 잘 맞는다. 게다가 기존에 훈련된 모델도 있으니 적용해서 결과보는 것도 쉽고 말이다.

## 아직 갈길이 더 먼..
그럼에도 아직 세밀한 부분은 떨어진다. 하지만, 그것보다, 이러한 특징들을 다른 곳에 활용할 수 있을 것 같아서 `아직 갈길이 더 먼...` 이라는 표현을 쓰고 싶다.
세상은 정말 무서운 속도로 빠르게 변하고 있다. `우리가 눈치채지 못하고 있더라도` 말이다.
