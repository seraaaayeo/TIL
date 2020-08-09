# Basic Machine Learning

* Hypothesis(가설함수) = Wx + b
* Cost function: 가설함수와 실제 데이터의 차의 제곱의 평균
* 머신러닝의 핵심은 cost가 최소화되는 W(가중치)를 찾는 과정이다.
    - Gradient descent

## Multi-variable Linear Regression
* 많은 변수를 표현하기 위해 Matrix를 사용한다.
* w1x1 + w2x2 + w3x3 +...
    - (x1 x2 x3)와  (w1 w2 w3)의 dot product
    - H(X) = XW
* 데이터의 건수 = instance
    - ![image](https://user-images.githubusercontent.com/53554014/89309773-ccfce200-d6ae-11ea-97ae-028da231da79.png)
    - 인스턴스(데이터) 5개, feature 3개
* matrix 연산은 행과 열의 개수가 매우 중요
    - 앞 행렬의 열과 뒷 행렬이 행이 일치해야 함.
    - (5X3) dot (3X1) = (5X1)
    - 즉 feature(변수)의 수와 weight의 수는 일치해야 한다.

## Logistic Regression
* **여기 설명 뭐라는지 잘 모르겟음... 복습할 것!**
* Binary Classification: 0(positive) 1(negative)
* Logistic vs Linear
    - Logistic: discrete(counted)
    > 신발사이즈
    - Linear: Continous(mesured)
    > 시간, 몸무게
* Logistic function(sigmoid)
    - logistic function의 출력값은 0과 1 사이이다.
    - 

## Softmax Regression
* hypothesis를 0과 1사이의 값으로 압축하면 좋겠다..!
* sigmoid(logistic) = 1 / 1+e^-2
* sigmoid 함수를 통과하면 0과 1사이의 출력값을 가진다.
* Logistic?
    - 두 데이터(혹은 그 이상)를 분류하기 위해 사용.
* Multinomial classificaion
    - 여러개의 binary classfication을 결합하여 찾을 수 있다.
* softmax
    - 각 클래스의 출력값은 **확률**이다.
    > 0과 1사이의 값이며, 각각의 출력값의 합은 1
    - one-hot encoding: 가장 큰 값을 1로, 나머지 값은 0으로 예측한다.
* Cross entropy

## Softmax classifier
* one-hot encoding
    * 한 가지의 데이터만 남겨둔다.
        - ex.([0], [3]): shape (2, 1)
        - one-hot encoding: [[[1,0,0,0,0,0,0]], [[0,0,0,1,0,0,0]]]
        - 즉, 차원이 하나 증가한다. 따라서 reshape 과정이 필요함.

* softmax function
    - 출력을 0~1 사이의 값으로 바꾼다.
    - 각 class의 출력값의 합은 1이다.(확률, probability)

* cross entropy: cost function
    ```
    Y * log(Y_hat)
    ```

* Gradient function
    * cost function을 최적화하는 방법(**Optimizer**)

## Softmax function을 이용한 개-고양이 분류기 만들기
* accuracy: 예측값이 실제와 얼마나 맞았는지에 대한 평균값.

## Application & Tips
### Contents
* Learning rate
* Data pre-processing
* Overfitting
* Data sets
* Learning
* Sample data

### Learning rate
cost를 최적화하는 과정(optimization)에서 한 번에 얼만큼 이동할 것인가에 대한 값.

* learning rate가 너무 작으면 모델의 속도가 느려진다.
* learning rate가 너무 크면 overshooting(cost가 오히려 증가하는 현상)이 발생할 수 있다.
    - epoch가 증가할수록 cost가 증가하기도 한다.
    - 학습이 잘 되지 않는 상황이다.
* 일반적으로 사용되는 learning rate는 0.01이다.
* learning rate decay
    - 학습에 진전이 없는 상황(cost가 줄어들지 않는 상황)에서 learning rate값을 조절함으로써 cost를 최소화하는 기법.
    - exponential decay, step decay 등

### Data preprocssing
* Feature scaling
    - Standardization(표준화): 평균으로부터 얼마나 떨어져 있는가(Mean distance)
    - Normalization(정규화): 0과 1사이의 값으로 나타내기
* Noisy data: 노이즈를 제거하고 의미있는 데이터만 남김으로써 정확한 모델을 만듦.

### Overfitting
* 학습이 반복될수록 모델의 정확도는 높아진다. 그러나 모델 학습에 쓰이지 않은 새로운 데이터(test)를 가지고 평가할 경우 accuracy가 낮아지는 경우가 있다.
* underfit(high bias): 학습이 덜 된 상태.
* overfit(high variance): 학습이 너무 많이 되어 주어진 데이터에**만** 맞게 학습이 된 상태.
* set a features
    - get more training data: 데이터를 많이 넣음으로써 변화량을 희석시킴.(fix high variance)
    - smaller set of feature: 의미 있는 공간에 데이터를 배치(차원을 줄임)함으로써 각각의 속성이 갖는 의미를 분명히 한다. 따라서 데이터를 학습시킬 때 그 의미를 통해 모델을 잘 찾을 수 있다.(fix high variance)
        - PCA
    - add additional feature: 모델 자체가 너무 심플할 때, 모델을 구체화하기 위해(fix high bias)
* regularization(add term to loss): loss값에 특정 값을 줌으로써 모델에 대해 특정 weight가 큰 값을 가진 때 weight를 정규화하는 방법.
* dropout
* batch normalization

### Data sets
* Training and Validation
    - Training: 학습을 위한 데이터.
    - Validation: 예측(테스트)에 사용되는 데이터, 평가를 위한 데이터
    - 머신러닝 모델을 만드는 데 데이터 구성을 하는 것이 중요하다.
* Evaluating a hypothesis
    - layer를 쌓고, learning rate와 optimizer를 적절히 설정한 후 (after fit parameters, select model), 새로운 데이터를 통해 모델을 검증하는 과정이 필요하다.
* Anomaly detection(이상 감지)
    - 건강한 데이터로 학습을 시켰을 경우 건강한 데이터에 대해서는 정확도가 높을 것이다. 이 경우에 새로운, 특이한 데이터를 넣었을 때 이를 잘 감지할 수 있는가.

### Learning
* Online VS Batch
    - Online: 인터넷이 연결된 상태에서 지속적으로 바뀌면서 학습
        - fresh data
        - connected network
        - weight tunning
        - model update
        - Infra(GPU) always
        - Realtime process application
        - Speed priority
    - Batch(offline): 데이터가 static한 상태에서 학습.
        - static data
        - disconnected network
        - weight initialize
        - model static
        - Infra(GPU) per call: 학습할 때만 요청해서 사용.
        - Stopping application
        - Corectness priority
* Fine tuning / Feature extraction
    - fine tuning: 기존의 모델에서 새로운 데이터를 학습시켜 weight값을 미세하게 조절하여 새로운 데이터에 대해 잘 구분해낼 수 있도록 함.
    - feature extraction: 기존 모델에 대해 새로운 task를 학습시켜 새로운 데이터를 잘 구분해낼 수 있도록 함.
* Efficient model: 실제 모델에 대한 performance가 중요.
    - Less inference time is needed
    - So we need light weight
    - Fully connected layer의 parameter값이 굉장히 많기 때문에 1X1 convolution으로 대체해서 사용(Squeezenet, Mobilenet 등)함으로써 속도를 높인다(performance를 높인다.)

### Sample data
* Fashion-MNIST
* IMDB
    - Text classfication
    - 영화평 긍정/부정 감정분석
* CIFAR-100
    - 100개의 클래스