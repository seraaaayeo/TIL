# Numpy 기초
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