# Convolutional Neural Network
* Forward Net, Fully Connected Network(전체가 연결되어 있음.)

## Basic idea
고양이에게 그림을 보여줬을 때 모든 뉴런이 반응하는 것이 아니라 일부분의 뉴런만 반응함을 알아냄에서 아이디어 착안.

* 전체 이미지를 하나의 입력으로 받지 않고, 이미지의 일부분만 입력으로 사용한다.
    - => **filter**
    - ex. 32X32X3 이미지를 5X5X3 filter
    - w,b값으로 인해 정의됨.
* filter 입력을 가지고 한 점을 뽑아낸다. 
    - => Wx+b
* filter를 옆으로 넘기면서(stride) 이미지 전체를 보며 점을 뽑아낸다.
    - => stride=2라는 것은 이미지를 두 칸씩 옆으로 넘긴다는 의미.
* 그렇다면 이 뽑아낸 점(output)은 몇 개일 것인가?
    - => ((N - F) / stride) +1
* filter를 적용할수록 이미지의 크기가 작아짐. = 이미지의 정보를 잃어버림.
    - => Padding
* 여러 개의 filter를 가지고 점(output)을 뽑은 것을 activation map(혹은 feature map)이라 한다.
    - ex. filter가 6개일 경우 깊이가 6이 된다.
* Pooling = Sampling
    ```
    - 깊이가 6인 conv. layer에서 한 레이어만 뽑아낸다.
    - 각 레이어에 대해 resize를 진행한다.
    - resize가 진행된 레이어를 다시 쌓는다.
    ```
    - 이 때 resize를 진행하는 방법을 pooling이라 하며, max pooling이 가장 많이 사용된다.
    - max pooling: 가장 큰 데이터를 뽑아낸다.

## CNN case study
1. LeNet-5
    - 5X5 filter, stride 1
    - 8 layers
    - 6개의 filter 사용, conv와 subsampling 진행
    - 출력 layer를 full connection함.
2. AlexNet
    - 96개 11X11 filter, stride 4
    - ReLU를 처음사용.
    - 7개의 CNN을 합쳐서 error를 낮춤.
3. GoogLeNet
    - Inception module
4. **ResNet**
    - 3.5% error, 2015
    - 152 layers => Fast forward 기법 사용하여 깊은 layer도 빠르게 학습.
    - gradient가 잘 전달될 수 있도록 지름길(shortcut)을 만들어 깊은 층을 가능하게 하는 네트워크 구조
    - 층이 깊어질수록 back propagation에서 gradient vanishing/exploding 문제가 발생할 수 있는데, ResNet의 기름길은 기울기 값을 그대로 더해지기 때문에 깊은 층을 쌓을 수 있다.
5. AlphaGo
    - 19X19X48 image, 48 feature planes.
    - First hidden layer는 zero pads해서 23X23 input으로 만듦.
    - 어쩌구저쩌구....

## CNN Basic Recap
Image Classification에서 가장 널리 사용되는 neural network, 3 종류의 layer(Convolution, pooling, fully connected layer).

* convloution layer, pooling layer => Feature extraction
* fully connected layer => Classification
    - 앞 레이어들에서 뽑아낸 특징들을 종합하여 해당 이미지가 어떤 이미지인지 판단하는 레이어.
* 입력으로 들어오는 channel과 fileter의 channel과 같아야 한다.
    - ex. input image: 32X32X3, filter: 5X5X3
* 입력 이미지와 filter를 convolution 연산하고 나온 output을 output feature map이라 한다. 컨볼루션 filter는 하나 이상 사용한다.
* 2D Convolution layer - 4D Tensors
* Stride: 한 번 컨볼루션 연산 후, 몇 칸 이동해서 다음 컨볼루션을 할 것인가
* Zero padding: 컨볼루션 하면 할수록 이미지 사이즈가 줄어들기 때문
* Activation function: ReLU(음수값을 0으로 만든다)
* 코드
    - ```tf.keras.layers.Conv2D```
    - __init__ method
        - filters: conv filter의 수, output channel을 몇으로 할 것인지
        - kernel_size: integer, tuple, list 가능
        - strides: interger, tuple, list 가능
        - padding: valid(No padding) / same(stride=1인 경우 기준으로 입력과 출력 size가 같아지게) 
        - data_format: (batch, height, width, channels)
    - convolution filter의 값을 지정하여 직접 만들고자 할 때
        - kernel dimension: {height, width, in_channel, out_channel}
    
## CNN Basic Pooling
- pooling layer: Channel별로 따로따로 연산 수행.
        - max pooling: ```max pool with 2X2 filters and stride 2```일 경우 2X2 필터 내의 4가지 데이터 중 가장 큰 값을 뽑는다.
        - average pooling: 4개 데이터의 평균값으로 뽑는다.
        - max pooling을 더 많이 쓴다. 큰 값이 convolution filter가 찾아내고자 하는 특징에 더 가까운 값이기 때문.
- 코드
    - ```tf.keras.layers.MaxPool2D```

## CNN Basic FC
- Fully connected layer = Dense layer
- 특징을 종합하여 판단을 내리는 역할을 한다.

## CNN Implementation Flow in Tensorflow
1. Set hyper *parameter 
    - learning rate, training epochs, batch size 등
2. Make a dara *pipelining 
    - dataset load, batch size만큼 데이터를 가져와서 네트워크에 공급하는 것.
3. Build a neural network model
    - 주로 tf.keras sequential APIs 사용
4. Define a *loss function
    - cross entropy
5. Calculate a gadient
    - tf.GradientTape
6. Select an optimizer
    - 계산된 gradient를 이용하여 weight를 업데이트(optimizer)하는 과정
    - Adam optimizer
7. Define a metric for model's *performance
    - accuracy
    - 학습 중간중간 학습이 잘 되고 있는지 확인
    - 학습이 끝나고 validation data, train data를 이용하여 학습이 얼마나 잘 되었는지 확인
8. Make a checkpoint for saving
9. Train and Validate a NN model

## CNN 코딩하기
* CNN의 입력으로는 4차원 tensor가 필요하다.
    - (batch, height, width, channel)