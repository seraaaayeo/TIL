## Docker
* [참고 자료](https://subicura.com/2017/01/19/docker-guide-for-beginners-1.html)
* 컨테이너 기반의 오픈소스 가상화 플랫폼.
* 컨테이너: 격리된 공간에서 프로세스가 동작하는 기술. 가상화 기술의 한 종류.
    - 기존의 가상화 방식
        - OS를 가상화(VM:Virtual Machine, Virtual Box)
        - 호스트 OS 위에 게스트 OS 전체를 가상화하여 사용한다.
        - ex.윈도우에서 리눅스 운영체제 사용 등.
    - 추가적인 OS를 설치하여 가상화하는 방법은 성능문제가 발생하기 때문에, 이를 개선하기 위해 프로세스를 격리하는 방식이 등장(container)
* 이미지: 컨테이터 실행에 필요한 파일과 설정값들을 포함하고 있는 것.
    - ex.우분투 이미지는 우분투를 실행하기 위한 모든 파일을 가지고 있고 MySQL 이미지는 debian을 기반으로 MySQL을 실행하는데 필요한 파일과 실행 명령어, 포트 정보 등을 포함.

### 도커 사용 이유
* [참고 자료](https://www.44bits.io/ko/post/why-should-i-use-docker-container)