# How to use Colab
### Contents
* Set GPU
* Google drive mount

## Set GPU
* 런타임 -> 런타임 유형 변경 -> GPU

## Google drive mount
1. 라이브러리를 사용하여 구글 드라이브 데이터 가져오기
    ```
    from google.colab import drive
    drive.mount('/content/drive/')
    ```
2. 구글 드라이브 파일 스트림 엑세스 허가
3. My drive/ 폴더 내부에 접근할 수 있는 데이터가 들어있음.
    - 원하는 데이터의 **경로 복사**를 사용

> 마운트하지 않고 데이터를 내려받아 사용할 경우 경로는 '/content/'
