---
layout: post
title: "Keras - Tokenizer base_filter”
description: ""
category:
tags: [deep learning, keras]
---
# Keras - Tokenizer base_filter()

링크는 여기에…

https://keras.io/preprocessing/text/#tokenizer

## Text Preprocessing
![](/assets/2017-01-12-Keras_-_Tokenizer_base_filter/F860E347-15C1-40A8-A51B-14E3243D3D70.png)

keras의 장점이면 몇가지 응용분야에 대한 preprocessing을 지원한다는 것이다.  

언어처리도 마찬가지이다.  

그 중에 어쩌면 가장 기본적인 기능인 Tokenizer를 보다 보니 `filters` 라는 옵션이 있다. 

게다가 default로 `filter=base_filter()` 라고 되어 있고, 

`base_filter`가 뭐하는 녀석인지는 전혀 설명이 없다. 

뭐 이름만 보면 기본적인 내용을 하는 것일텐데, 아무래도 궁금해서 참을 수 없었다.

코드를 뒤져보자.

## Code

링크는 여기에…

[keras/text.py at master · fchollet/keras · GitHub](https://github.com/fchollet/keras/blob/master/keras/preprocessing/text.py)

어??

코드가 사라졌다!!!

[keras/text.py at 9f4734cbf1044cb5eb921f8e834423c3f528d0d4 · fchollet/keras · GitHub](https://github.com/fchollet/keras/blob/9f4734cbf1044cb5eb921f8e834423c3f528d0d4/keras/preprocessing/text.py)

하루 사이에 패치가 발생해서 base_filter()가 사라졌다. ㅠ.ㅠ

실제 코드상을 보면 

```python
def base_filter():
    f = string.punctuation
    f = f.replace("'", '')
    f += '\t\n'
    return f
```

인데 string.punctuation을 보면 특수부호들이 다 들어가있다. 여기에 `’`만 뺀 리스트를 보내서, 실제로 tokenizer가 돌 때 얘들은 제거해서 돌리는 역할을 한다.

이제는 패치가 일어나서 이해하기 쉬워졌는데 그전에는 진짜 진짜 알아보기 힘들었음;;
췟;

암튼, 결론은

> filters로 속해있는 char는 진짜로 날려버린다는 의미.  
> 아직 doc은 updated되지 않았는데 곧 되겠지. ㅠ.ㅠ 뭔가 엄청 허무하다. 그래도 이걸 보느냐고 날린 시간이 있는데…  

