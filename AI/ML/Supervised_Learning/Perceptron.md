# 퍼셉트론(Perceptron)
* 인공신경망 시스템. 입력이 있을 때, 어떤 함수에 따라서 activation이 일어나고 출력을 하는 시스템.
* 퍼셉트론 -> 인공 신경망 -> 인공지능 으로 진행된다.
* 구조
    ```
    출력 = activation(w1x1 + w2x2 + B) #w1, w2 = 가중치, B = bias
    ```
    - activation function(step function) : 특정 조건을 만족하면 1을 출력(활성화). 이외에는 0을 출력.
    - 퍼셉트론은 논리 게이트의 역할을 한다.
* 논리게이트
    - AND
    - NAND(Not-And): 0/0 -> 1, 1/0 -> 1, 0/1 -> 1, 1/1 -> 0
* 단층 퍼셉트론: 선형 분류기
* 다층 퍼셉트론: 비선형 분류기
    - 퍼셉트론을 여러개 쌓아서 만든다.
    - OR와 NAND 게이트를 결합하여 비선형인 XOR 게이트를 만들어 구역을 분리할 수 있다.
    - 여기서 NAND 게이트와 OR 게이트를 hidden layer라고 한다.
    - 이처럼 여러 개의 layer를 이용하면 세분화된 분리가 가능하다.
    - **Hidden layer가 3층 이상이면 Deep Neural Network(DNN, 딥러닝)이라 한다.**