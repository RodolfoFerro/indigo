---
title: "A simple linear regression with TensorFlow 2.0"
subtitle: Let's adjust that y=m*x+b equation...
layout: post
date: 2020-06-20 03:00
tag:
  - Python
  - Artificial Neurons
  - Neural Networks
  - TensorFlow
headerImage: false
projects: true
hidden: false # don't count this post in blog pagination
description: A simple linear regression with TensorFlow 2.0
category: blog
author: rodferro
---


# Linear regression

A very simple approach to perform a linear regression with a single neuron using Keras.

### Package import


```
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('ggplot')
```

### Random data generation

We create our samples.


```
x = np.linspace(0, 50, 51)
x
```




    array([ 0.,  1.,  2.,  3.,  4.,  5.,  6.,  7.,  8.,  9., 10., 11., 12.,
           13., 14., 15., 16., 17., 18., 19., 20., 21., 22., 23., 24., 25.,
           26., 27., 28., 29., 30., 31., 32., 33., 34., 35., 36., 37., 38.,
           39., 40., 41., 42., 43., 44., 45., 46., 47., 48., 49., 50.])



And for each sample add some random noise for the $y$ value.


```
y = x + 10 * np.random.random((len(x)))
y
```




    array([ 4.59333333, 10.1888939 ,  3.10342612,  3.78295369, 10.57957367,
            8.31186454, 11.97466834,  8.38350117, 14.58165746, 12.7179244 ,
           16.04800824, 16.04253531, 17.7570093 , 15.36504093, 23.32077078,
           19.38063338, 25.72030949, 20.81364232, 18.55875267, 25.1340618 ,
           28.48036   , 21.73467374, 30.81790828, 28.56736033, 28.83225669,
           28.18684725, 34.95836113, 29.90731219, 30.90521404, 38.67280311,
           33.28501437, 40.01292045, 33.16216509, 34.99748693, 35.87077378,
           35.66317699, 36.37898628, 42.26194454, 47.36216501, 45.62434907,
           46.47169133, 48.05329522, 45.83970327, 50.68483177, 53.01284414,
           54.96997999, 46.42993498, 50.41667051, 53.26256812, 58.97071734,
           55.3635401 ])



The generated data looks like this:


```
plt.scatter(x, y, label='Generated  data')
plt.legend()
plt.show()
```


![png](../assets/posts/Linear_regression_files/Linear_regression_8_0.png)


### Modelling

The model has just a single neuron that will model the linear equation $y = mx + b$.

The trained weight will correspond to the slope $m$ of the equation and the bias to the intersection value $b$.


```
model = tf.keras.Sequential()
model.add(tf.keras.layers.Dense(1, input_shape=[1]))
model.compile(loss='mean_squared_error', optimizer=tf.keras.optimizers.Adam(0.1))
```


```
model.summary()
```

    Model: "sequential"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    dense (Dense)                (None, 1)                 2         
    =================================================================
    Total params: 2
    Trainable params: 2
    Non-trainable params: 0
    _________________________________________________________________


We proceed to fit the model.


```
history = model.fit(x, y, epochs=200)
```

    Epoch 1/200
    2/2 [==============================] - 0s 4ms/step - loss: 653.8051
    Epoch 2/200
    2/2 [==============================] - 0s 2ms/step - loss: 399.1392
    Epoch 3/200
    2/2 [==============================] - 0s 2ms/step - loss: 205.5257
    Epoch 4/200
    2/2 [==============================] - 0s 2ms/step - loss: 83.4503
    Epoch 5/200
    2/2 [==============================] - 0s 2ms/step - loss: 23.8983
    Epoch 6/200
    2/2 [==============================] - 0s 2ms/step - loss: 14.8980
    Epoch 7/200
    2/2 [==============================] - 0s 2ms/step - loss: 30.8598
    Epoch 8/200
    2/2 [==============================] - 0s 2ms/step - loss: 53.7728
    Epoch 9/200
    2/2 [==============================] - 0s 2ms/step - loss: 69.0219
    Epoch 10/200
    2/2 [==============================] - 0s 2ms/step - loss: 70.0617
    Epoch 11/200
    2/2 [==============================] - 0s 2ms/step - loss: 58.6065
    Epoch 12/200
    2/2 [==============================] - 0s 2ms/step - loss: 43.6842
    Epoch 13/200
    2/2 [==============================] - 0s 2ms/step - loss: 26.3015
    Epoch 14/200
    2/2 [==============================] - 0s 2ms/step - loss: 15.8109
    Epoch 15/200
    2/2 [==============================] - 0s 1ms/step - loss: 12.0864
    Epoch 16/200
    2/2 [==============================] - 0s 2ms/step - loss: 13.2904
    Epoch 17/200
    2/2 [==============================] - 0s 2ms/step - loss: 17.2666
    Epoch 18/200
    2/2 [==============================] - 0s 2ms/step - loss: 20.2788
    Epoch 19/200
    2/2 [==============================] - 0s 1ms/step - loss: 21.0044
    Epoch 20/200
    2/2 [==============================] - 0s 2ms/step - loss: 19.3135
    Epoch 21/200
    2/2 [==============================] - 0s 2ms/step - loss: 16.5099
    Epoch 22/200
    2/2 [==============================] - 0s 1ms/step - loss: 13.8078
    Epoch 23/200
    2/2 [==============================] - 0s 1ms/step - loss: 12.4786
    Epoch 24/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.5450
    Epoch 25/200
    2/2 [==============================] - 0s 2ms/step - loss: 12.2430
    Epoch 26/200
    2/2 [==============================] - 0s 2ms/step - loss: 12.6910
    Epoch 27/200
    2/2 [==============================] - 0s 2ms/step - loss: 13.0053
    Epoch 28/200
    2/2 [==============================] - 0s 1ms/step - loss: 12.8281
    Epoch 29/200
    2/2 [==============================] - 0s 1ms/step - loss: 12.4289
    Epoch 30/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.6947
    Epoch 31/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.3287
    Epoch 32/200
    2/2 [==============================] - 0s 2ms/step - loss: 11.3578
    Epoch 33/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.3632
    Epoch 34/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.5163
    Epoch 35/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.5517
    Epoch 36/200
    2/2 [==============================] - 0s 2ms/step - loss: 11.4354
    Epoch 37/200
    2/2 [==============================] - 0s 2ms/step - loss: 11.2493
    Epoch 38/200
    2/2 [==============================] - 0s 2ms/step - loss: 11.0766
    Epoch 39/200
    2/2 [==============================] - 0s 2ms/step - loss: 11.0697
    Epoch 40/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.9828
    Epoch 41/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.0126
    Epoch 42/200
    2/2 [==============================] - 0s 1ms/step - loss: 11.0186
    Epoch 43/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.9801
    Epoch 44/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.9340
    Epoch 45/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.7914
    Epoch 46/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.7687
    Epoch 47/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.6795
    Epoch 48/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.6936
    Epoch 49/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.6416
    Epoch 50/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.6058
    Epoch 51/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.5609
    Epoch 52/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.5371
    Epoch 53/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.4772
    Epoch 54/200
    2/2 [==============================] - 0s 3ms/step - loss: 10.4357
    Epoch 55/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.4067
    Epoch 56/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.3866
    Epoch 57/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.3872
    Epoch 58/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.3384
    Epoch 59/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.3408
    Epoch 60/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.3051
    Epoch 61/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.2206
    Epoch 62/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.1830
    Epoch 63/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.2140
    Epoch 64/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.1338
    Epoch 65/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.1010
    Epoch 66/200
    2/2 [==============================] - 0s 1ms/step - loss: 10.0534
    Epoch 67/200
    2/2 [==============================] - 0s 2ms/step - loss: 10.0265
    Epoch 68/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.9996
    Epoch 69/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.9761
    Epoch 70/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.9521
    Epoch 71/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.9255
    Epoch 72/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.8958
    Epoch 73/200
    2/2 [==============================] - 0s 4ms/step - loss: 9.8855
    Epoch 74/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.8750
    Epoch 75/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.8222
    Epoch 76/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.7902
    Epoch 77/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.7729
    Epoch 78/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.7519
    Epoch 79/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.7254
    Epoch 80/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.7084
    Epoch 81/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6988
    Epoch 82/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6648
    Epoch 83/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6532
    Epoch 84/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6367
    Epoch 85/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6036
    Epoch 86/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.6125
    Epoch 87/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.5628
    Epoch 88/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.5510
    Epoch 89/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.5662
    Epoch 90/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.5147
    Epoch 91/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.5191
    Epoch 92/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.5031
    Epoch 93/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.4601
    Epoch 94/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.4431
    Epoch 95/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.4269
    Epoch 96/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.4388
    Epoch 97/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.3951
    Epoch 98/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.4153
    Epoch 99/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.3706
    Epoch 100/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.3629
    Epoch 101/200
    2/2 [==============================] - 0s 4ms/step - loss: 9.3394
    Epoch 102/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.3237
    Epoch 103/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.3269
    Epoch 104/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.3081
    Epoch 105/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2812
    Epoch 106/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2657
    Epoch 107/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2867
    Epoch 108/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2592
    Epoch 109/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2355
    Epoch 110/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2726
    Epoch 111/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2075
    Epoch 112/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.2053
    Epoch 113/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1904
    Epoch 114/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1810
    Epoch 115/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1972
    Epoch 116/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1841
    Epoch 117/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1773
    Epoch 118/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1964
    Epoch 119/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1943
    Epoch 120/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1598
    Epoch 121/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1316
    Epoch 122/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1139
    Epoch 123/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1245
    Epoch 124/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1076
    Epoch 125/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.0872
    Epoch 126/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1018
    Epoch 127/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0746
    Epoch 128/200
    2/2 [==============================] - 0s 4ms/step - loss: 9.0583
    Epoch 129/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1542
    Epoch 130/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.1178
    Epoch 131/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0470
    Epoch 132/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0456
    Epoch 133/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0353
    Epoch 134/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0327
    Epoch 135/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0275
    Epoch 136/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0258
    Epoch 137/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0356
    Epoch 138/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0048
    Epoch 139/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0333
    Epoch 140/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0226
    Epoch 141/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0144
    Epoch 142/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0049
    Epoch 143/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9832
    Epoch 144/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9752
    Epoch 145/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0019
    Epoch 146/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.0445
    Epoch 147/200
    2/2 [==============================] - 0s 4ms/step - loss: 8.9637
    Epoch 148/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9682
    Epoch 149/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9812
    Epoch 150/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9747
    Epoch 151/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9863
    Epoch 152/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9593
    Epoch 153/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9487
    Epoch 154/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9373
    Epoch 155/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9841
    Epoch 156/200
    2/2 [==============================] - 0s 1ms/step - loss: 9.1398
    Epoch 157/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0232
    Epoch 158/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9637
    Epoch 159/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9288
    Epoch 160/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9415
    Epoch 161/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9729
    Epoch 162/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9534
    Epoch 163/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9379
    Epoch 164/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9516
    Epoch 165/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9502
    Epoch 166/200
    2/2 [==============================] - 0s 2ms/step - loss: 9.0555
    Epoch 167/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9306
    Epoch 168/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9888
    Epoch 169/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9640
    Epoch 170/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9570
    Epoch 171/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9267
    Epoch 172/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9134
    Epoch 173/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9231
    Epoch 174/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9520
    Epoch 175/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9192
    Epoch 176/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9162
    Epoch 177/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9310
    Epoch 178/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9030
    Epoch 179/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9056
    Epoch 180/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9027
    Epoch 181/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9037
    Epoch 182/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8955
    Epoch 183/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9029
    Epoch 184/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9420
    Epoch 185/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9328
    Epoch 186/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9198
    Epoch 187/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9586
    Epoch 188/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8910
    Epoch 189/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8981
    Epoch 190/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.9199
    Epoch 191/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9941
    Epoch 192/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9090
    Epoch 193/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8938
    Epoch 194/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9167
    Epoch 195/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9029
    Epoch 196/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8897
    Epoch 197/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8889
    Epoch 198/200
    2/2 [==============================] - 0s 1ms/step - loss: 8.8904
    Epoch 199/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.8932
    Epoch 200/200
    2/2 [==============================] - 0s 2ms/step - loss: 8.9216


And we can plot the loss during the training.


```
plt.plot(history.history['loss'])
plt.show()
```


![png](../assets/posts/Linear_regression_files/Linear_regression_15_0.png)


### Model prediction

There are two ways to generate the adjusted model. The first one will be simlpy to use the `.predict()` method directly over the $x$ samples:


```
y_pred_model = model.predict(x)
```


```
plt.scatter(x, y, label='Generated data')
plt.plot(x, y_pred_model, label='Predicted with model', color='c')
plt.legend()
plt.show()
```


![png](../assets/posts/Linear_regression_files/Linear_regression_18_0.png)


The second (and my favorite) way is to understand the guts inside the network and access the information to literally replicate the model.

In this case we acces the first (and only) layer:


```
layer = model.get_layer(index=0)
layer
```




    <tensorflow.python.keras.layers.core.Dense at 0x7fe81910e828>



Then, we get and print the weights and biases:


```
weights = layer.get_weights()
weights
```




    [array([[1.014319]], dtype=float32), array([4.2396894], dtype=float32)]



As we previously mentioned, the only weight will correspond to the slope and the bias to the intersection point. In order to replicate the linear equation we simply do:


```
m, b = weights[0][0], weights[1]
print(m)
print(b)
```

    [1.014319]
    [4.2396894]



```
y_pred_params = m * x + b
y_pred_params
```




    array([ 4.23968935,  5.25400829,  6.26832724,  7.28264618,  8.29696512,
            9.31128407, 10.32560301, 11.33992195, 12.35424089, 13.36855984,
           14.38287878, 15.39719772, 16.41151667, 17.42583561, 18.44015455,
           19.4544735 , 20.46879244, 21.48311138, 22.49743032, 23.51174927,
           24.52606821, 25.54038715, 26.5547061 , 27.56902504, 28.58334398,
           29.59766293, 30.61198187, 31.62630081, 32.64061975, 33.6549387 ,
           34.66925764, 35.68357658, 36.69789553, 37.71221447, 38.72653341,
           39.74085236, 40.7551713 , 41.76949024, 42.78380919, 43.79812813,
           44.81244707, 45.82676601, 46.84108496, 47.8554039 , 48.86972284,
           49.88404179, 50.89836073, 51.91267967, 52.92699862, 53.94131756,
           54.9556365 ])




```
plt.scatter(x, y, label='Generated data')
plt.plot(x, y_pred_params, label='Line fitted using parameter values', color='c')
plt.legend()
plt.show()
```


![png](../assets/posts/Linear_regression_files/Linear_regression_26_0.png)

If you want to run the code above directly on Google Colab, please follow [this link](https://colab.research.google.com/drive/1zC47uLBWbc2BOPlwxFAxENTxc7irVCND?usp=sharing).
