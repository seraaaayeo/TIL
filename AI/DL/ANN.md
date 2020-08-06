# Tensorflow로 딥러닝 구현하기
### 데이터 용어 정리
* Epoch: 한 번의 epoch는 전체 데이터 셋에 대해 한 번 학습을 완료한 상태를 뜻한다.
* Batch: 나눠진 데이터 셋. iteration은 epoch를 나누어서 실행하는 횟수를 뜻한다. 
    - 데이터셋의 양이 굉장히 많기 때문에 데이터셋을 여러 작은 데이터로 쪼개서 학습을 진행하며, 이 작은 데이터를 batch, 쪼갠 데이터의 양을 batch size라 한다.
    - 예: 1000개의 데이터를 batch size 100으로 학습을 시킬 경우, 1 epoch는 10 iteration

## 데이터 준비하기
* Dataset API를 사용하여 데이터 준비.
```
data = np.random.sample((100, 2)) #shape이 (100,2)
labels = np.random.sample((100, 1))

#numpy array로부터 데이터셋 생성
dataset = tf.data.Dataset.from_tensor_slices((data, lables))
dataset = dataset.batch(32)
```

## 딥러닝 모델 생성
* 인공신경망 Sequential 모델을 만들기 위한 함수
    ```
    tf.keras.models.Sequential()
    ```
* 신경망 모델의 layer 구성에 필요한 함수
    ```
    tf.keras.layers.Dense(units, activation)
    ```
    - unit: 레이어 안의 Node 수
    - activation: 적용할 활성함수
* 예시 **tf.keras.layers를 추가하여 hidden layer를 쌓는다.**
    ```
    model = tf.keras.models.Sequential([
     tf.keras.layers.Dense(10, input_dim=2, activation='sigmoid'),
     tf.keras.layers.Dense(10, activation='sigmoid'),
     tf.keras.layers.Dense(1, activation='sigmoid'),
    ]
    ```
    - input node는 2개
    - 첫 번째 layer의 node는 10개
    - 두 번째 layer의 node는 10개
    - 세 번째 layer의 node는 1개.
    - 각 unit은 weight로 연결된다.
* 모델 학습하기
    - loss function, optimizer(loss function을 줄이는 전략이 무엇인가) 필요.
    ```
    #모델 구성
    model.compile(loss='mean_squared_error', optimizer='SGD') #학습 방법 설정
    model.fit(dataset, epochs=100) #모델 학습
    
    #데이터셋 생성
    dataset_test = tf.Dataset.from_tensor_slices((data_test, labels_test))
    dataset_test = dataset_test.batch(32)
    
    #모델 성능 평가
    model.evaluate(dataset_test)
    predicted_labels_test = model.predict(data_test) #학습된 모델로 예측값 생성
    ```
    - SGD: Statistic(??) Gradient Descent

### 분류모델: 네이버 영화 댓글 평점 데이터
* Data -> Preprocessing -> Input layer
    * Preprocessing: Tokenizing&Bow, Encoding
* softmax function을 통해 긍정인지 부정인지 경향성을 볼 수 있다.
* 최적화 기법: 선형회귀에서는 GD가 쓰이지만, 인공신경망에서는 다양한 형태의 GD 기법들이 사용된다.
    - **SGD**, **Adam**, Momentum, AdaGrad, RMSProp 등
