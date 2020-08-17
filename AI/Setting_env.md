# How to set Environment for Machine Learning & Deep Learning
## Trouble Shooting
* ImportError: DLL load failed when trying import ssl
* Why we should create anaconda virtual environment?
* conda install tensorflow vs pip install tensorflow
* Why I can't use packages I installed?

### ssl import error
```
(base) C:\Users\User>jupyter notebook
Traceback (most recent call last):
File "C:\Users\User\anaconda3\envs\tf2\Scripts\jupyter-notebook-script.py", line 6, in <module>
    from notebook.notebookapp import main
File "C:\Users\User\anaconda3\envs\tf2\lib\site-packages\notebook\notebookapp.py", line 66, in <module>
    from tornado import httpserver
File "C:\Users\User\anaconda3\envs\tf2\lib\site-packages\tornado\httpserver.py", line 29, in <module>
    import ssl
File "C:\Users\User\anaconda3\envs\tf2\lib\ssl.py", line 98, in <module>
    import _ssl             # if we can't import it, let the error propagate
ImportError: DLL load failed: 지정된 프로시저를 찾을 수 없습니다.
```
* 위와 같은 에러가 발생하여 주피터를 실행할 수가 없었음.
* Trial and error
    - Install OpenSSL and set env path: 연구실 컴퓨터는 주피터가 정상적으로 작동하는데, 연구실 컴퓨터에는 OpenSSL이 환경변수 path로 설정되어 있음을 발견하여 노트북에도 해당 폴더를 설치하고 환경변수를 설정 => **Failed**
    - Set anaconda path at env path: [github issue](https://github.com/jupyter/notebook/issues/4332)를 참고하여 환경변수 path에 Anaconda/Library/bin을 추가 => **Failed**
    - ```Conda config --set ssl_verify False```: [블로그](https://happy-chipmunk.tistory.com/entry/Windows-10-Anaconda-Geopandas-80-%EC%84%A4%EC%B9%98-%EC%A4%91-HTTP-000-connection-%EB%AC%B8%EC%A0%9C-Failed-with-initial-frozen-solve-%EB%AC%B8%EC%A0%9C)를 참고함 => **Failed**
    - ```conda install openssl``` : openssl이 아나콘다에 설치가 안 되었나 해서 설치해봄 => **Failed**
* [Solution](https://gldmg.tistory.com/142)
    - "아나콘다경로/Library/bin/" 경로 열기
    - 다음 네 가지 파일들을 복사
        - libcrypto-1_1-x64.dll
        - libcrypto-1_1-x64.pdb
        - libssl-1_1-x64.dll
        - libssl-1_1-x64.pdb
    - "아나콘다경로/DLLs/" 경로에 붙여넣기

### Anaconda 가상환경
* [아나콘다에서 가상환경을 사용하는 이유와 가상환경 생성](https://chancoding.tistory.com/85)
* tensorflow2를 사용하기 위해 가상환경을 tf2로 생성하였다.
* ```conda list```로 설치된 패키지 확인 결과, 파이썬 3.8이 설치되었음을 확인
* **Purpose**: python 3.7, tensorflow 2 환경

### conda install tensorflow
![image](https://user-images.githubusercontent.com/53554014/90393562-f7e22f80-e0cb-11ea-971f-034b903901f0.png)

```
(base) conda create -n tf2 python=3.7
(base) activate tf2
(tf2) conda install tensorflow
```
* tensorflow 2버전 이상에서는 conda를 사용한 tensorflow 설치가 권장된다.

### tf2 가상환경에서 jupyter notebook 사용하기
```
(tf2) conda install jupyter notebook
```
* jupyter notebook은 base(root)를 바탕으로 실행된다(jupyter가 base에 설치되어 있기 때문). 따라서 가상환경에도 jupyter를 설치해줘야 한다.
* Problem: tf2 가상환경에서는 ssl import에러가 다시 발생.
* Reason: 위의 DLLs에 dll 파일 복사한 것은 base 환경이기 때문.
* [Solution](https://zvi975.tistory.com/65): tf2 환경에도 마찬가지로 Libary/bin의 4가지 dll과 pdb 파일을 복사하여 DLLs에 붙여넣어야 함.

### jupyter notebook 실행
```
(tf2) jupyter notebook
```
* tensorflow 확인
    - tf2 환경에서 실행된 주피터에서 파일을 생성한다.
    - ![image](https://user-images.githubusercontent.com/53554014/90386718-ef83f780-e0bf-11ea-9854-8f4a98c7e311.png)

