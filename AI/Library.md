# Contents
* scikit-learn
* tensorflow
* keras
* numpy

***
# Scikit-learn

## 사이킷런 차트시트

![scikit-learn chartsheet.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/97e9d01c-e74f-42f9-80fb-9417f482aedd/Screenshot_from_2020-08-24_13-54-11.png)

- 사이킷런 알고리즘 Task
    - Regression
    - Classification
    - Clustering
    - Dimensionality reduction
- 알고리즘을 나누는 기준
    - 데이터의 종류(수치형 데이터(Quantity), 범주형 데이터(Category))
    - 라벨의 유뮤(정답의 유무)
    - 데이터 수량

## 사이킷런의 주요 모듈

### 데이터 표현 API

|  <center>Category</center> |  <center>Module name</center> |  <center>Description</center> |
|:--------|:--------:|:--------:|
|**데이터셋**| <center>sklearn.datasets</center> | <center>사이킷런에서 제공하는 정제된 데이터셋</center> |
|**데이터 타입**| <center>sklearn.utils.Bunch</center> | <center>사이킷런에서 제공하는 데이터셋의 데이터 타입(자료형)</center> |
|**데이터 전처리**| <center>sklearn.preprocessing</center> | <center>데이터 전처리(정규화, 인코딩, 스케일링 등)</center> |
|**데이터 분리**| <center>sklearn.model_selection.train_test_split</center> | <center>학습용 / 테스트용 데이터셋 분리</center> |
|**평가**| <center>sklearn.metrics</center> | <center>분류, 회귀, 클러스터링 알고리즘의 성능을 측정하는 함수 제공</center> |
|**모델**| <center>sklearn.ensemble</center> | <center>앙상블관련 머신러닝 알고리즘 - 랜덤 포레스트, 에이다 부스트, 그래디언트 부스팅</center> |
|**모델**| <center>sklearn.linear_model</center> | <center>선형 머신러닝 알고리즘 - 릿지, 라쏘, SGD 등</center> |
|**모델**| <center>sklearn.naive_bayes</center> | <center>나이브 베이즈 관련 머신러닝 알고리즘</center> |
|**모델**| <center>sklearn.neighbors</center> | <center>최근접 이웃 모델 관련 - 릿지, 라쏘, SGD 등</center> |
|**모델**| <center>sklearn.svm</center> | <center>SVM 관련 머신러닝 알고리즘</center> |
|**모델**| <center>sklearn.tree</center> | <center>트리 관련 머신러닝 알고리즘 - 의사결정 트리 등</center> |
|**모델**| <center>sklearn.cluster</center> | <center>군집 관련 머신러닝 알고리즘</center> |

### 데이터 표현법

사이킷런에서 제공하는 데이터셋은 Numpy의 **ndarray**, Pandas의 **DataFrame**, SciPy의 **Sparse Matrix**를 이용해 나타낼 수 있다.

사이킷런에서는 데이터 표현 방식을 **특성행렬(Feature Matrix)과 타겟벡터(Target Vector)** 두 가지로 나타낸다.

![sklearn pic.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d6fa07b7-fa5e-4caa-8b43-7a64be1b8179/Screenshot_from_2020-08-24_15-35-11.png)

- 특성행렬(Feature Matrix)
    - 입력 데이터를 의미
    - Feature : 데이터에서 수치 값, 이산 값, 불리언 값으로 표현되는 개별 관측치.
    - Sample : 각 입력 데이터

- 타겟 벡터(Target Vector)
    - 입력 데이터의 **라벨(정답)**
    - 목표(Target) : 특성 행렬(Feature Matrix)로부터 예측하고자 하는 것
    - 타겟 벡터는 보통 1차원 벡터로 나타낸다.

### Datasets 모듈

[https://scikit-learn.org/stable/datasets/index.html#datasets](https://scikit-learn.org/stable/datasets/index.html#datasets)

- `sklearn.datasets` 은 **dataset loaders**와 **dataset fetchers**로 나뉘며, 각각 `Toy dataset` 과 `Real Word dataset`을 제공
- Toy dataset
    - `datasets.load_boston()` : 회귀, 미국 보스턴 집값 예측
    - `datasets.load_breast_cancer()` : 분류 문제, 유방암 판별
    - `datasets.load_digits()` : 분류 문제, 0~9 숫자 분류
    - `datasets.load_iris()` : 분류 문제, 붓꽃 품종 분류
    - `datasets.load_wine()` : 분류 문제, 와인 분류

### Toy dataset - wine data 분석
```
from sklearn.datasets import load_wine

data = load_wine()
data.keys()
>> dict_keys(['data', 'target', 'frame', 'target_names', 'DESCR', 'feature_names'])
```
1. `data` : 특성 행렬(feature matrix)

    ```
    data.data.shape
    >> (178, 13) #데이터가 178개, 특성이 13개이다.

    data.data.ndim
    >> 2 # 2차원이다.
    ```
    - 행 : 데이터의 개수(n_samples) 열 : 특성의 개수(n_features)

2. `target` : 타겟 벡터

    ```
    data.target

    	>> array([0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
    	       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
    	       0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1,
    	       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
    	       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,
    	       1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2,
    	       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
    	       2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2,
    	       2, 2])
    ```

    - 타겟 벡터는 1차원
    - 타겟 벡터의 길이는 특성 행렬의 데이터 개수와 일치해야 한다.(특성 데이터의 정답(라벨)이 타겟 벡터이기 때문!)

3. `feature_names` : 특성들의 이름

    ```
    data.feature_names

    >> ['alcohol',
    	 'malic_acid',
    	 'ash',
    	 'alcalinity_of_ash',
    	 'magnesium',
    	 'total_phenols',
    	 'flavanoids',
    	 'nonflavanoid_phenols',
    	 'proanthocyanins',
    	 'color_intensity',
    	 'hue',
    	 'od280/od315_of_diluted_wines',
    	 'proline']
    ```
    - 이 와인 데이터의 13개의 특성 이름이 저장되어 있다.

4. `target_names` : 분류하고자 하는 대상

    ```
    data.target_names

    >> array(['class_0', 'class_1', 'class_2'], dtype='<U7')
    ```
    - 데이터를 각각 class_0, class_1, class_2로 분류한다.

5. `DESCR` : Describe의 약자임

***

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