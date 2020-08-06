# Tensorflow
```
conda install tensorflow
```
* 전세계에서 가장 많이 쓰이는 딥러닝 프레임워크.
* Tensor = 다차원 array = Data
    - 딥러닝에서 텐서는 다차원 배열로 나타내는 데이터이다.
    - ex.RGB 이미지는 3차원 배열로 나타나는 텐서.
* Flow: 데이터의 흐름. 
    - 입력 tensor가 있을 때, operation node에 의해 결과값이 나오는 텐서의 흐름을 tensorflow
    - 텐서플로우에서 계산은 데이터 플로우 그래프로 수행한다.
    * 모델을 만든다 = graph를 만든다.

## Tensorflow 사용

### 상수 선언하기
```
import tensorflow as tf

tensor_constant = tf.constant(value, dtype=None, shape=None, name=None)
```
* value: 반환되는 상수값
* shape: tensor의 차원(optional)
* dtype: 반환되는 tensor 타입(optional_)
* name: 상수 이름(optional)
* 예
    - 모든 원소 값이 0인 tensor 생성
    ```
    tensor_zero = tf.zeros(shape, dtype=tf.float32, name=None)
    shape에는 차원의 튜플을 넣는다. 예를 들어 2X2 텐서를 생성하고 싶으면 (2,2) 입력.
    ```
    - 모든 원소 값이 1인 tensor 생성
    ```
    tensor_one = tf.ones(shape, dtype=tf.float32, name=None)
    ```

### 시퀀스 선언하기
* start에서 stop까지 증가하는 num 개수 데이터
    ```
    import tensorflow as tf

    tensor_seq = tf.linspace(start, stop, num, name=None)
    ```
    * start: 시작 값
    * stop: 끝 값
    * num: 생성할 데이터 개수
    * name: 시퀀스 이름
* start에서 stop까지 delta씩 증가하는 데이터
    ```
    tensor_seq2 = tf.range(start, limit=None, delta=None, name=None)
    ```
    * limit: 끝 값
    * delta: 증가량

### 난수 선언하기
* 보통 난수를 통해서 모델을 초기화한다.
* 주로 정규분포 사용.
```
import tensorflow as tf

#정규분포 생성
tensor_ = tf.random.normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name='normal')

#균등분포 생성
tensor2_ = tf.random.uniform(shape, minval=0, maxval=None, dtype=tf.float32, seed=None, name='uniform')
```
* seed: seed값에서 특정한 알고리즘을 통해 순차적으로 난수 생성.
* 균등분포: 일정한 범위 내의 확률은 모두 같다.

### 변수 선언하기
```
#정규분포 생성
tensor_val = tf.Variable(value, name=None)

#일반적인 퍼셉트론의 가중치와 bias 생성
weight = tf.Variable(10)
bias = tf.Variable(tf.random.normal([10, 10]))
```
* 모델을 트레이닝해서 얻고싶은 값이 무엇이냐
* 초기화된 변수에 트레이닝을 통한 값이 assign 가능.
* 가중치를 variable로 선언하면 모델이 training하면서 가중치가 update 가능.

### Tensor 연산자
* 단항 연산자
    * tf.negative(x) #숫자 
    * tf.logical_not(x) #!x, Boolean
    * tf.abs(X)
* 이항 연산자
    * add, subtract, multiply
    * 나누기: truediv
    * 몫: mod
    * 제곱: pow
* tensor에 .numpy()를 붙이면 넘파이 배열로 변환.

***

# Keras
딥러닝 모델을 만들기 위한 고수준의 API 요소를 제공하는 모델 수준의 라이브러리

* Keras API
    - multi-backend
    - cpu, gpu 모두 구동

***

# 아나콘다와 텐서플로우
* [아나콘다 가상환경 생성](https://zvi975.tistory.com/65)

***

# Numpy
* 행렬이 왜 필요한가? -> 머신러닝에서 대부분의 데이터는 행렬로 표현됨.
* 행렬을 어떻게 표현할까? -> numpy array

## Numpy Array
```
import numpy as np
A = np.array([[1, 2], [3, 4]])
```
* 산술연산: 큰 데이터를 다룰 때 편의를 위해 만들어진 기능이다.
* 비교연산
* 논리연산
    ```
    a = np.array([1, 1, 0, 0], dtype=bool) //TTFF
    ```
* norm(normalization)
    - 원소의 합이 1이 되도록 한다.
    - 벡터를 벡터 원소의 합으로 나눈다.
    - A = A/np.sum(A)
* reduction
    - argmin/argmax: 최소/최대값의 **인덱스**를 반환
    - min/max: 최소/최대값을 반환
* logical reductions
    - all: array내의 모든 값이 True인가?
    - any: array내의 값이 하나라도 True인가?
* Statistical reductions
    - mean
    - median
    - std: standard devation, 표준편차
* dot product
    ```
    np.dot(x, y)
    ```
* 전치행렬: 행과 열을 뒤집은 행렬.
    ```
    A = np.array([][])
    
    print(A.transpose())
    print(A.T)
    ```
* 역행렬: Numpy의 선형대수학 세부패키지 linalg를 사용.
    ```
    np.linalg.inv()
    ```

## Numpy 그림 그리기
1. 캔버스
    * 그래프 공간(캔버스) 설정
    ```
    xrange=[1, 3] //x축 범위
    yrange=[2, 4] //y축 범위
    ```
2. 그림 그리기
    * 어떤 함수 f와 매우 작은 숫자 threshold에 대해
    * 캔버스 내에 점 P = (x, y)를 임의로 생성
    * f(P) < threshold라면 점을 찍는다.
    * 이를 100,000회 반복한다.
3. 원 그리기
    * (0, 0)이 중심이고 반지름 1인 원을 그리는 방정식은 다음과 같다.
    ```
    x^2+y^2=1
    ```
    * 원을 그리는 함수를 circle이라 정의하자.
    * 정확히 원 위에 있는 점들에 대해 circle(P)는 0이어야 한다.