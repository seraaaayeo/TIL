# Basic Deep Learning

## Concept
우리의 뇌는 어떻게 작용하는 것인가?

* 신호(x)는 각각 다른 양으로 들어온다(x * weight)
* 각 돌기에서 들어온 신호가 합쳐진다(sum)
* 뉴런을 통과할 때 bias되어 그 다음으로 통과한다.
* 어느 값 이상이 되면 활성화(activation)된다.

## 딥러닝의 역사와 발전
* 첫 번째 침체기: XOR 문제
* MLP(Multi Layer Perceptron)
* Backpropagation
* CNN(Convolutional Neural Network)
    - 고양이에게 그림을 보여줬을 때, 그림의 모양에 따라 일부의 뉴런만 활성화 되는 것을 발견
    - 일부 뉴런만 활성화가 된 후, 그것이 조합되는 방식으로 진행하는 것이 아닐까?
    - CNN: 이미지의 부분 부분을 잘라서 보낸 후 합치는 방법
* 두 번째 침체기: 레이어가 깊으면 역전파 방법으로 전달되는 error가 층을 지나갈수록 흐려지며, 오히려 간단한 네트워크에서 잘 동작함.
* SVM, RandomForest
* Breakthrough(2006, 2007)
    - 초기값을 잘 주면 deep한 네트워크도 학습할 수 있다.
    - deep한 네트워크를 이용하면 아주 복잡한 문제도 해결할 수 있다.
    - Neural Network라는 이름이 들어간 논문은 리젝되던 시기였기 때문에, 용어를 Deep Net, Deep Learning으로 바꿈.
    - 이후 다시 신경망이 주목을 받으며 연구되기 시작.
* Image Net: Large Scale Visual Recognition Challenge
    - 그림을 주었을 때 어떤 그림인지 맞추는 챌린지.
    - 2012년에 오류율을 15.3%로 떨어트림(AlexNet)
    - 2015년에 3%대로 떨어짐.

## XOR 문제를 Neural Network로 해결하기
* 두 개의 unit으로 구성된 하나의 NN으로 해결 가능하다.
    - 이 때 W, B는 주어졌다.
    - 어떻게 Weight와 Bias를 자동화할 수 있을 것인가?
* **최적의 Weight와 Bias 찾는 방법(Optimazation, cost를 줄이는 방법) 중 하나: Gradient Descent**
* Backpropagation
    - 예측값과 실제값 사이에서 나오는 오류(cost)를 뒤로부터 앞으로 전달시켜 실제 적용해야 하는 값을 찾는다.
    - 미분값: x, w, b가 각각 y(출력값)에 미치는 영향
        > Chain rule: f(g(x)) = af/ag * ag/ax
    - 기본 term의 미분값만 알 수 있으면 아무리 복잡한 식도 구할 수 있다.
* Tensorboard: data를 가지고 model을 만드는 과정에서 w, b, loss 등을 시각화해주는 도구.

## Sigmoid와 Relu
* Neural Network: 실제 값(ground-truth)와 모델의 결과(output)와의 차이(loss)를 미분(gradient)하여 Back-propagation 방법으로 w, b를 학습시켜 나가는 과정.
* sigmoid function의 문제점: network가 deep해질수록 더 많은 sigmoid가 필요하게 되고, 여러 개의 sigmoid를 곱하면서 각 함수의 gradient값이 0에 가까워지므로(vanishing gradient) 결과적으로 소실되어 학습을 시킬 수가 없게 된다.

### Relu(**Lab 10-1: Sigmoid보다 ReLU가 더 좋아** 강의 참고. 여태까지의 이해 안 된 설명을 가장 잘 설명해줌.)
f(x) = max(0, x)

* 역시나 문제가 있다.
    - 0보다 작을 때 -> gradient가 0이다.(아예 전달되지 않는다.)
    - 그럼에도 불구하고 성능이 매우 좋기 때문에 많이 쓰인다.
* ```tf.keras.activations``` -> ```sigmoid, tanh, relu, elu, selu```
* ```tf.keras.layers``` -> ```leaky relu```
* 참고: tensorflow는 eager모드와 setion모드로 실행할 수 있는데, eager 모드가 강력하게 권고된다. 2버전은 eager모드가 default이지만 1버전에서는 ```tf.enable_eager_execution()```을 필수로 추가해야 함.

### Create network - MNIST
* class 타입으로 네트워크 정의하기
    * 주의사항: tf.keras.Model을 상속해줘야 함.
* argmax: 이 logit과 label에서 가장 큰 값의 위치가 어딘지 알려줘라.
    - one hot encoding을 했기 때문에 **위치**가 필요한 것임.
    - MNIST 데이터를 사용하기 때문에 '7' 라벨을 one hot encoding하여 [0,0,0,0,0,0,0,1,0,0]로 변환해서 '위치'값으로 변환했기 때문(컴퓨터 연산을 용이하게 하기 위해)
* tf.cast를 통해 prediction을 숫자값으로 바꿔준다.
    - accuracy(평균, reduce_mean 사용)를 구하기 위해
* eager mode
    - checkpoint 만들기
        - 네트워크가 중간에 끊겼을 때 어디부터 다시 학습할 것인가에 많이 사용.
        - 또는 데이터를 시각화하는 등에서 어느 지점 데이터를 로드하기 위해 사용.

## Weight Initialization
### 초기화 방법
* Local Minima, Saddel Point를 피해 Global Minima를 찾을 수 있도록 시작지점을 잘 설정하는 방법.
* Xavier Initialization
* He Initialization for ReLU
    - Xavier(glorot_uniform) Init: Variance = 2/(Channel_in + Channel_out)
    - He Initializaion: Varaince = 4/(Channer_in + Channel_out)
        - Relu함수에 최적화된 weight 초기화 방법.

## Dropout
* 사용하는 이유
    - Under-fitting: 트레이닝 데이터셋에 네트워크가 매우 안 맞음.
        - 트레이닝 데이터셋의 정확도 낮음
        - 테스트 데이터셋의 정확도 낮음.
    - Over-fitting: 모든 트레이닝 데이터셋에 네트워크를 맞춤.
        - 트레이닝 데이터셋의 정확도 높음.
        - **테스트 데이터셋의 정확도 낮음.**
        - 트레이닝 데이터셋에만 너무 맞추다 보니, 다른 데이터(테스트 데이터)가 들어올 경우 맞출 수 없는 상황.
    - 이러한 상황을 피할 수 있도록 regulazation을 하는 방법 중 하나가 dropout이다.
* 모든 뉴런(node)을 사용하여 학습하는 게 아니라, 일부 node를 사용하지 않고 학습.
* Regulazion: 일부 node를 이용하여 학습한 후, 모든 node를 이용하여 판단(예측)한다.
    - 고양이의 일부(귀 모양, 발톱, 눈 모양 등)만 가지고 학습을 한 후, 예측할 때는 모든 부분을 가지고 예측하기 때문에 트레인 데이터랑 완전히 다른 데이터에도 적절하게 예측할 수 있다.
    - 즉, 그때그때 학습할 뉴런을 랜덤하게 선택하여 영향력이 지나치게 강한 뉴런(학습데이터에 지나치게 의존되어 새로운 데이터에 대한 예측력이 떨어지는 뉴런)들을 배제할 수 있는 가능성을 높이면서 과적합을 방지하는 방법이다.
* 사용할 node는 random하게 정한다.

## Batch Normalization
* Internal Covariate Shift: Distribution이 network의 layer를 지나면서 망가진다. 따라서 해당 이미지가 원래 어떤 이미지였는지 잘 알 수 없게 되어 학습률이 떨어진다.
* Batch normalization: 이러한 현상을 방지하기 위한 방법.
    - input으로 들어오는 distribution을 계속 normalization 시켜 일정하게 만든다.
    