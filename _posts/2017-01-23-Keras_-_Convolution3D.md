# Keras - Convolution3D
링크는 여기에…
[Convolutional Layers - Keras Documentation](https://keras.io/layers/convolutional/#convolution3d)


## 기본 폼
```python
keras.layers.convolutional.Convolution3D(nb_filter, kernel_dim1, kernel_dim2, kernel_dim3, init='glorot_uniform', activation=None, weights=None, border_mode='valid', subsample=(1, 1, 1), dim_ordering='default', W_regularizer=None, b_regularizer=None, activity_regularizer=None, W_constraint=None, b_constraint=None, bias=True)
```

2D를 써봤다면 별 다를 것 없다.


## Arguments

역시 다를 것이 없다.  
다만 kernel이 3차원으로 늘어나서 그 부분에 대한 argument가 늘어난 부분과,  
subsample tuple에 차원이 증가된 정도 되겠다.  

정리할 내용도 크게 없으니, 이와 함께 쓸 max pooling도 같이 보자.

# MaxPooling3D
링크는 여기에…

[Pooling Layers - Keras Documentation](https://keras.io/layers/pooling/#maxpooling3d)

## 기본폼
```python
keras.layers.pooling.MaxPooling3D(pool_size=(2, 2, 2), strides=None, border_mode='valid', dim_ordering='default')
```

## Arguments
pool_size에 차원 늘어난 것이 전부..정도 되겠다.

## 정리
3차원으로 늘리는 것은 크게 문제가 되지 않을 것으로 보인다. 다만,  
이게 3차원 모두 대칭인 데이터가 아니긴 한데, 그래도 같은 사이즈로 pooling하는 수 밖에 없을 것 같다.  
방법이 없으니..@.@  
특별히 주의할 점을 없을 것으로 보인다.